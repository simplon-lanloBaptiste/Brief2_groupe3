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
![addRule]()

Install OK,  
Créer fqdn pour accéder à distance  
