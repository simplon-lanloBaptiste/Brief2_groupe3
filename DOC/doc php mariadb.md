### Installation de PHP :  

En suivant le [guide d'installation de NextCloud](https://docs.nextcloud.com/server/latest/admin_manual/installation/source_installation.html#prerequisites-for-manual-installation), nous avons dans un premier temps identifié quels composants / programmes étaient déjà installés. PHP est présent en version 1, nous avons choisi d'installer la version la plus récente en 8.0  en suivant [ce guide](https://linuxize.com/post/how-to-install-php-8-on-ubuntu-20-04/) qui explique bien les prérequis et les étapes d'installation de PHP et de ses diffétents modules.  

Les commandes utilisées sont :  
```console
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
```
Pour retrouver la liste de tous les modules déjà installés :
```console
php8.0 -m
```


</br>
</br>


### Installation MariaDB

```console
    sudo apt update
    sudo apt install mariadb-server
    sudo mysql_secure_installation
```

démarrage du service MariaDB

```console
groupe3@VMBDDB2G3:~$ sudo systemctl start mariadb
```

check du démarrage du service MariaDB :
```console
groupe3@VMBDDB2G3:~$ sudo systemctl status mariadb
```
Création de la base de données :  
```console

```
