### ***1- Créer un workspace Azure Sentinel et y envoyer les logs de tous les serveurs*** 
___
Création et configuration du sentinel workspace :  

![sentinelWorkspaceCreate](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/420f35b0484e9e33c1b909be22bcc17b1c1623b2/IMG/SENTINEL/screen0_create_sentinel_workspace.png)

Une fois le workspace sentinel créé, associer les 3 VMs :  

![linkVMsToSentinel](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/420f35b0484e9e33c1b909be22bcc17b1c1623b2/IMG/SENTINEL/screen1_link_VMs_to_sentinel.png)   

Vérification de la connexion des VMs au workspace Sentinel :  

![VMConnected](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/420f35b0484e9e33c1b909be22bcc17b1c1623b2/IMG/SENTINEL/screen2_VMs_are_linked.png)  

Installation de l'agent sentinel sur la vm Admin : récupération des fichiers via wget  

```console
sudo wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w f2931f26-ef9b-4e32-b7e9-91f2f209b759 -s uN6ReK/2anYLaJM+Gify8XmA8ZwHydNA+miyivhjbq1AyMsKx+wCfmMATM16rTkttDMn0LI9ssYEf9lYDAHPLA== -d opinsights.azure.com
```  

Tous les éléments ont été télécharges sur le /home, dont un script python pour l'installation de l'agent, à exécuter :  
```console
sudo ./onboard_agent.sh
```

Lors de l'installation, un message indique qu'il manque des prérequis, à savoir gdb (GNU Debugger) et python, qui sont donc à installer :  

```console
aptget install gdb  
sudo apt-get install -y python2
```  

Tous les logs sont configurables ici :  

```console
groupe3@VMAppliB2G3:/etc/opt/microsoft/omsagent/sysconf/omsagent.d$ ll
total 88
drwxr-xr-x 2 root root 4096 Jul 11 13:02 ./
drwxr-xr-x 3 root root 4096 Jul 11 13:02 ../
-rw-r--r-- 1 root root 1689 Jun  8 23:28 apache_logs.conf
-rw-r--r-- 1 root root  774 Jun  8 23:28 auditlog.conf
-rw-r--r-- 1 root root  893 Jun  8 23:28 change_tracking.conf
-rw-r--r-- 1 root root  412 Jun  8 23:28 change_tracking_inventory.mof
-rw-r--r-- 1 root root  117 Jun  8 23:28 collectd.conf
-rw-r--r-- 1 root root  233 Jun  8 23:28 heartbeat.conf
-rw-r--r-- 1 root root 1062 Jun  8 23:28 mongo.conf
-rw-r--r-- 1 root root  576 Jun  8 23:28 monitor.conf
-rw-r--r-- 1 root root  981 Jun  8 23:28 mysql.conf
-rw-r--r-- 1 root root 2712 Jun  8 23:28 mysql_logs.conf
-rw-r--r-- 1 root root  185 Jun  8 23:28 oms.conf
-rw-r--r-- 1 root root  826 Jun  8 23:28 operation.conf
-rw-r--r-- 1 root root 1680 Jun  8 23:28 patch_management.conf
-rw-r--r-- 1 root root  368 Jun  8 23:28 patch_management_inventory.mof
-rw-r--r-- 1 root root  986 Jun  8 23:28 postgresql_logs.conf
-rw-r--r-- 1 root root  316 Jun  8 23:28 statsd.conf
-rw-r--r-- 1 root root  164 Jun  8 23:28 syslog.conf
-rw-r--r-- 1 root root  252 Jun  8 23:28 telemetry.conf
-rw-r--r-- 1 root root  192 Jun  8 23:28 update_management.conf
-rw-r--r-- 1 root root  606 Jun  8 23:28 vmware_esxi.conf
```


### ***2- Créer une ressource Application Insights liée au workspace Sentinel et ajouter un test de disponibilité pour monitorer l’application***  
___


### ***3- Mettre en place TLS avec un certificat Let’s Encrypt sur le port tcp/443***  
___

