Pour créer un utilisateur nextCloud :  

*Lien vers la [doc nextCloud](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/occ_command.html#user-commands)*  
</br>
Depuis la VM Appli :  

Création d'un groupe "users" et d'un groupe "admins" :  
```console
groupe3@VMAppliB2G3:/var/www/nextcloud$ sudo -u www-data php occ group:add users
Created group "users"
groupe3@VMAppliB2G3:/var/www/nextcloud$ sudo -u www-data php occ group:add admins
Created group "admins"
```
Création de 4 users admins (Luna, Baptiste, Ryan, Alain)  

La variable d'environnement par défaut pour le mdp nextCloud est "OC_PASS", il faut se connecter en ROOT, sinon la variable d'environnement en question n'est pas gardée.  
Aller dans le répertoire "nextcloud", dans notre cas : /var/www/nextcloud  

```console
export OC_PASS=************
su -s /bin/sh www-data -c 'php occ user:add --password-from-env --display-name="Alain" alain'
```  
Pour ajouter, puis vérifier l'appartenance a un groupe :  
```console
sudo -u www-data php occ group:adduser admins alain
sudo -u www-data php occ group:list
```  
Nous pouvons retrouver les users créés dans la VM BDD :  

```console
MariaDB [nextcloudDB]> select UID from oc_accounts;
+----------+
| UID      |
+----------+
| Ryan     |
| alain    |
| baptiste |
+----------+
```