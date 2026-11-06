# Instruments de music

lien vers le repos : https://github.com/John-Dav9/musics_tools

## Etape 1

#### Installation sous WSL2 de Windows 11 du projet instruments de musique:

Ouvrir Powershell et l'ouvrir (ou l'installer) ou n'importe quelle console

    wsl

    sudo apt update

    # PHP 8.4
    sudo apt install php8.4-common php8.4-{bcmath,bz2,curl,gd,gmp,intl,mbstring,opcache,readline,xml,zip}

    # node.js 22.22
    sudo apt install nodejs

    wget https://get.symfony.com/cli/installer -O - | bash
    # puis
    mv /home/VOTRE_LOGIN/.symfony5/bin/symfony /usr/local/bin/symfony

    npm install -g --allow-scripts=@anthropic-ai/claude-code @anthropic-ai/claude-code

    cd /home/VOTRE_LOGIN/

    symfony check:requirement

    # Modifier si nécessaire

    symfony new instruments_de_musique --version=lts --webapp
    # ou cloner le répertoire

    cd instruments_de_musique

## Etape 2 Initialisation de claude 

    claude update
    claude

Suivre le serveur, puis dans Claude

    /init