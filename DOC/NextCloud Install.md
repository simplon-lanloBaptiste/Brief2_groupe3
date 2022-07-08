[Documentation pour installer NextCloud en ligne de commande](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/occ_command.html#command-line-installation-label)  

```console
sudo -u www-data php occ maintenance:install 


CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin1234';

sudo -u www-data php occ  maintenance:install --database="mysql" --database-name="nextcloudDB" --database-user="admin" --database-pass="admin1234" --database-host="10.0.3.6" --database-port="22" --admin-user="admin" --admin-pass="admin1234" --data-dir="/var/www/nextcloud/data"                          
```
Ajout du port 8080 dans les fichiers conf d'apache2 :  

  483  vi /etc/apache2/sites-enabled/nextcloud.conf  
  484  vi /etc/apache2/sites-enabled/000-default.conf  
  501  sudo vi /etc/apache2/ports.conf  
  502  vi /etc/apache2/sites-enabled/nextcloud.conf  

ajout d'une règle sur vmAppli concernant le port 8080  
![addRule](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/af495c2a20c45b873641f511b99f7f96ac5d4271/IMG/PORTCHANGE/screen_8080_1_AddRule.png)  

Install OK,  
http://20.118.188.191:8080/nextcloud/index.php/login  

penser à créer fqdn pour accès à distance  

https://docs.microsoft.com/en-us/azure/virtual-machines/create-fqdn
