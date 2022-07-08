Placer l'archive récupérée sur le site de nextcloud sur la VM Admin, possible via Filezilla (nous mettrons l'archive dans le /home)  

![fileZillaConnect]()
![FileZillaPut]()
![FileZillaCheck]()

Récupérer le chemin absolu vers l'archive à déplacer vers la vm Appli :  
```console
groupe3@VMAdminB2G3:~/ncfiles$ readlink -f latest.tar.bz2
/home/groupe3/ncfiles/latest.tar.bz2
```  
Puis se connecter en sftp à la VM Appli et uploader l'archive vers le /home de la vm distante :  
```console
groupe3@VMAdminB2G3:~/ncfiles$ sftp groupe3@10.0.3.5
Connected to 10.0.3.5.
sftp> put /home/groupe3/ncfiles/latest.tar.bz2
Uploading /home/groupe3/ncfiles/latest.tar.bz2 to /home/groupe3/latest.tar.bz2
/home/groupe3/ncfiles/latest.tar.bz2                                       100%  118MB  87.8MB/s   00:01
```
Ensuite se connecter à la VM Appli et vérifier l'existence du fichier dans le /home :  
```console
groupe3@VMAppliB2G3:~$ ls -lrt|grep tar
-rwxrw-r-- 1 groupe3 groupe3 123445625 Jul  8 11:49 latest.tar.bz2
```


extraction des fichiers nextCloud avec la commande "tar" :  (x pour extract, v pour verbose : donne un récap des actions de la commande en temps réel, f pour "file", -C pour indiquer le chemin vers où extraire le fichier)  

```console
sudo tar xvf ./latest.tar.bz2 -C /var/www/nextcloud/
 [...]
 nextcloud/3rdparty/microsoft/azure-storage-blob/src/Blob/Models/AccessCondition.php
nextcloud/3rdparty/microsoft/azure-storage-blob/src/Blob/Models/DeleteBlobOptions.php
nextcloud/3rdparty/microsoft/azure-storage-blob/src/Blob/Models/UndeleteBlobOptions.php
nextcloud/3rdparty/microsoft/azure-storage-blob/src/Blob/Models/CreateContainerOptions.php
nextcloud/3rdparty/microsoft/azure-storage-blob/src/Blob/Models/CreateBlockBlobOptions.php
nextcloud/3rdparty/microsoft/azure-storage-blob/src/Blob/Models/CopyState.php
nextcloud/3rdparty/microsoft/azure-storage-blob/src/Blob/Models/GetBlobPropertiesResult.php
[...]
```  

Quand la console rend la main, se placer dans le bon répertoire et vérifier la présence des fichiers :  

```console
groupe3@VMAppliB2G3:/var/www/nextcloud/nextcloud$ ls -la
total 176
drwxr-xr-x 14 nobody nogroup  4096 Jun 20 15:29 .
drwxr-xr-x  3 root   root     4096 Jul  8 09:27 ..
-rw-r--r--  1 nobody nogroup  3253 Jun 20 15:01 .htaccess
-rw-r--r--  1 nobody nogroup   101 Jun 20 15:01 .user.ini
drwxr-xr-x 43 nobody nogroup  4096 Jun 20 15:29 3rdparty
-rw-r--r--  1 nobody nogroup 19327 Jun 20 15:01 AUTHORS
-rw-r--r--  1 nobody nogroup 34520 Jun 20 15:01 COPYING
drwxr-xr-x 48 nobody nogroup  4096 Jun 20 15:07 apps
drwxr-xr-x  2 nobody nogroup  4096 Jun 20 16:01 config
-rw-r--r--  1 nobody nogroup  4095 Jun 20 15:01 console.php
drwxr-xr-x 22 nobody nogroup  4096 Jun 20 15:41 core
-rw-r--r--  1 nobody nogroup  6260 Jun 20 15:01 cron.php
drwxr-xr-x  2 nobody nogroup 12288 Jun 20 15:01 dist
-rw-r--r--  1 nobody nogroup   156 Jun 20 15:01 index.html
-rw-r--r--  1 nobody nogroup  3456 Jun 20 15:01 index.php
drwxr-xr-x  6 nobody nogroup  4096 Jun 20 15:01 lib
-rw-r--r--  1 nobody nogroup   283 Jun 20 15:01 occ
drwxr-xr-x  2 nobody nogroup  4096 Jun 20 15:01 ocm-provider
drwxr-xr-x  2 nobody nogroup  4096 Jun 20 15:01 ocs
drwxr-xr-x  2 nobody nogroup  4096 Jun 20 15:01 ocs-provider
-rw-r--r--  1 nobody nogroup  3139 Jun 20 15:01 public.php
-rw-r--r--  1 nobody nogroup  5340 Jun 20 15:01 remote.php
drwxr-xr-x  4 nobody nogroup  4096 Jun 20 15:01 resources
-rw-r--r--  1 nobody nogroup    26 Jun 20 15:01 robots.txt
-rw-r--r--  1 nobody nogroup  2452 Jun 20 15:01 status.php
drwxr-xr-x  3 nobody nogroup  4096 Jun 20 15:01 themes
drwxr-xr-x  2 nobody nogroup  4096 Jun 20 15:07 updater
-rw-r--r--  1 nobody nogroup   382 Jun 20 15:28 version.php
```  


