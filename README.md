#!/usr/bin/env bash

#_______________________________________________________________________#
# ----------------------------- VARIÁVEIS ----------------------------- #
#_______________________________________________________________________#

PASTA_DOWNLOADS="HOME/$USER/Downloads/programas"
URL_OPERA="https://download3.operacdn.com/pub/opera/desktop/85.0.4341.18/linux/opera-stable_85.0.4341.18_amd64.deb"


#_______________________________________________________________________#
# ----------------------------- REPOSITÓRIOS----------------------------#
#_______________________________________________________________________#

## Removendo travas eventuais do apt ##
sudo rm /var/lib/dpkg/lock-frontend
sudo rm /var/cache/apt/archives/lock
## Atualizando o repositório ##
sudo apt update -y

#repositório spotify
curl -sS https://download.spotify.com/debian/pubkey_5E3C45D7B312C643.gpg | sudo apt-key add -
echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list

#_______________________________________________________________________#
# ----------------------------- DOWNLOADS-------------------------------#
#_______________________________________________________________________#
mkdir $PASTA_DOWNLOADS
wget "$URL_OPERA" -p $PASTA_DOWNLOADS
wget "$URL_LIBREOFFICE" -p $PASTA_DOWNLOADS
sudo dpkg -i $PASTA_DOWNLOADS/*.deb
#tar -xzf "$ARQUIVO_LIBREOFFICE"

sudo apt install snapd
sudo snap install spotify
sudo snap install libreoffice


#_______________________________________________________________________#
# ----------------------------- Finalização-----------------------------#
#_______________________________________________________________________#

## Finalização, atualização e limpeza##
sudo apt update && sudo apt dist-upgrade -y
flatpak update
sudo apt autoclean
sudo apt autoremove -y


printf "Finalizado!\n"
