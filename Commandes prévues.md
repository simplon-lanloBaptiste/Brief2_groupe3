Liste des commandes prévues à utiliser pour le Brief 2 (a linker dans Collaborative Note)


Insérer et activer les clés SSH publiques dans le serveur :
    https://superuser.com/questions/671077/how-to-use-ssh-public-key-with-putty-to-connect-to-a-linux-machine


Pour mettre les clés ssh dans authorized_keys
vim ./.ssh/authorized_keys

Pour créer les nouvelles clés sur le server Admin pour les serveurs Appli et BDD et pousser les clés publiques d'Admin sur Appli et BDD et d'Appli sur BDD.
    https://linuxhint.com/generate-ssh-keys-on-linux/

Pour copier la clé publique SSH sur une autre VM
    ssh-copy-id username@host-ip-address

Création du nom de domaine personnalisé
https://docs.microsoft.com/en-us/azure/virtual-machines/custom-domain

PHP
https://linuxize.com/post/how-to-install-php-8-on-ubuntu-20-04/

Pour info ; lister les modules php installés :
    php -m

Pour voir la version de php :
    php -v
    apt list --installed | grep php