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

### ***2- Créer une ressource Application Insights liée au workspace Sentinel et ajouter un test de disponibilité pour monitorer l’application***  
___


### ***3- Mettre en place TLS avec un certificat Let’s Encrypt sur le port tcp/443***  
___

