Pour créer le fqdn de notre VM Appli :  
Directement depuis Azure, dans la ressource "-ip" de la vm Appli, "setting" > "configuration" :  

![fqdn](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/dc5dc961dc143cc1938902187467e4aef3ad2292/IMG/FQDN_DNS/sreen0_add_fqdn.png)  

Une fois que le fqdn est défini, il faut l'autoriser dans le fichier de configuration php de nextCloud :  
```console
groupe3@VMAppliB2G3:~$ cd /var/www/nextcloud/config
groupe3@VMAppliB2G3:/var/www/nextcloud/config$
groupe3@VMAppliB2G3:/var/www/nextcloud/config$ vim config.php

<?php
$CONFIG = array (
  'passwordsalt' => 'jMndOay3FiTnfEynClAg8DXmHhtMXc',
  'secret' => 'I4JSt4ZI7RWepUdPTxW2AbAyW0Aa3CyErFqCI52G44O3xRP/',
  'trusted_domains' =>
  array (
    0 => 'localhost','20.118.188.191','groupe3.westus3.cloudapp.azure.com'
  ),

```

Restart du daemon apache2  
(sudo systemctl restart apache2)  

le fqdn "groupe3.westus3.cloudapp.azure.com" a été ajouté dans le "array" trusted domain, le site nextcloud est désormais accessible via son fqdn.