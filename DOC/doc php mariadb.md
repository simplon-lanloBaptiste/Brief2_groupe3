### 1. Installation de PHP :  

En suivant le [guide d'installation de NextCloud](https://docs.nextcloud.com/server/latest/admin_manual/installation/source_installation.html#prerequisites-for-manual-installation), nous avons dans un premier temps identifié quels composants / programmes étaient déjà installés. PHP est présent en version 1, nous avons choisi d'installer la version la plus récente en 8.0  en suivant [ce guide](https://linuxize.com/post/how-to-install-php-8-on-ubuntu-20-04/) qui explique bien les prérequis et les étapes d'installation de PHP et de ses diffétents modules.  

Les commandes utilisées sont :  
```console
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt install php8.0
```
Pour continuer nous avons retrouvé la liste de tous les modules déjà installés :  

```console
php8.0 -m
```  

![phpModuleList](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/MARIADB/1_screen1_PHP_modulesList.png)  

Ensuite nous avons identifié les modules prérequis à l'installation de NextCloud manquants et les avons installés manuellement via la commande :  
```console
sudo apt install php8.0-[nom du module]
```  

### 2. Installation MariaDB  
</br>
Sur la vm BDD  

```console
sudo apt update
sudo apt install mariadb-server
sudo mysql_secure_installation
```
![installMariaDB1](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/MARIADB/0_screen1_InstallMariaDB.png)  

![installMariaDB2](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/MARIADB/0_screen2_InstallMariaDBRootPWD.png)  

![installMariaDB3](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/MARIADB/0_screen3_InstallMariaDBAnonymousUser.png)  

![installMariaDB4](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/MARIADB/0_screen4_InstallMariaDBLastSteps.png)  


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
MariaDB [(none)]> CREATE DATABASE G3B2BDD;
Query OK, 1 row affected (0.000 sec)

MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| G3B2BDD            |
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.000 sec)
```
