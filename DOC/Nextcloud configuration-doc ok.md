# Apache Web server configuration sur VM Appli

## Création du fichier nextcloud.conf

Créer le fichier "nextcloud.conf" à l'aide d'un "touch" et la commande 

    sudo touch /etc/apache2/sites-available/nextcloud.conf

"sudo" car /etc/ est protégé.

![Nexcloud.conf 1](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/Nextcloud.conf%201.png)

Utiliser VIM pour éditer le nouveau fichier "nextcloud.conf" et rajouter les informations nécessaire en changeant, si besoin, les chemins d'accès:

    Alias /nextcloud "/var/www/nextcloud/"

    <Directory /var/www/nextcloud/>
      Require all granted
      AllowOverride All
      Options FollowSymLinks MultiViews

        <IfModule mod_dav.c>
            Dav off
        </IfModule>
    </Directory>

A l'aide cette commande :

    vim /etc/apache2/sites-available/nextcloud.conf

![Nexcloud.conf 2](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/Nextcloud.conf%202.png)

![Nexcloud.conf 3](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/Nextcloud.conf%203.png)


Créer le dossier nextcloud dans "var/www/" avec "sudo" car protégé et vérification de sa présence et des droits avec "ls -la".

    sudo mkdir var/www/nextcloud

![Nexcloud.conf 4](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/Nextcloud.conf%204.png)

Activer le module "mod_rewrite" avec la commande : (en sudo à nouveau pour permissions)

    sudo a2enmod rewrite

Ce qui permet de mettre à jour le lien symbolique d'Apache vers sa bibliothèque.

![Nexcloud.conf 5](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/Nextcloud.conf%205.png)

Redémarer le démon Apache avec la commande :

    sudo systemctl reload apache2

![Nexcloud.conf 6](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/Nextcloud.conf%206.png)

Vérifier que le démon tourne bien

    ps -ef | grep apache

![Nexcloud.conf 7](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/Nextcloud.conf%207.png)


(Tutoriel suivi : https://docs.nextcloud.com/server/latest/admin_manual/installation/source_installation.html#additional-apache-configurations)