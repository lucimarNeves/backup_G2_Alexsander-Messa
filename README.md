#!/bin/bash



clear
Menu(){
   echo "-----------------------------------------------------"
   echo "    Linux Comandos para Backup entre maquinas        "
   echo "-----------------------------------------------------"
   echo
   echo "[  1  ] Informe arquivo para backup"
   echo "[  2  ] Backup "
   echo "[  3  ] Sair"
   echo
   echo -n "Qual a opcao desejada ? "
   read opcao
   case $opcao in
      1) Arquivo ;;
      2) Backup ;;
      3) exit ;;
      *) "Opcao desconhecida." ; echo ; Principal ;;
   esac
}

Arquivo(){

clear  #comando linux para limpar
ls -lah #comando linux para listar de forma humana
echo "Deseja mostrar qual o tipo de arquivo"
read tipo
file $tipo #comando linux para indicar qual o tipo de arquivo
echo "Pressione enter para voltar ao menu"
read vazio
clear
  Menu
}

                          

Backup() {
echo "Informe usuário remoto" 
read USR #VARIAVEL PARA CAPTURA DO USUARIO DE DESTINO
clear
echo "Informe IP de destino"
read ip #VARIAVEL PARA CAPTURA DO IP DE DESTINO
clear
SRC=/home/aluno #VARIAVEL PARA DEFINIR A ORIGEM

clear
rsync -ah --stats --progress -e ssh $SRC $USR@$ip:$DIR #BACKUP DE ORIGEM PARA DESTINO REMOTO

rsync -ah --stats --progress -e ssh $USR@ip:$SRC $DIR #BACKUP LOCAL

rsync -ah --stats --progress -e ssh $SRC $DIR /home/aluno/Área\ de\ Trabalho/Lucimar_2/ #RETORNO DE ARQUIVOS COPIADOS PARA MAQUINA LOCAL

rsync -v -e  ssh -p22 --progress /home/aluno/ aluno@$ip #BACKUP REMOTO NA MAQUINA DE DESTINO
echo "Backup realizado com sucesso"
read pause
clear
  Menu
}

Menu
