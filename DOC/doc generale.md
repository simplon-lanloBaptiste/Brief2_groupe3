# Création d'une VM via le portail Azure


## Informations basiques  

All resources > Create > Virtual machine  

![creating a vm](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/creating%20a%20VM.png)  

Choisir "subscription" et "resource group"  

![subres](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/subres.png)  

Choisir un nom pour la VM, la "Region" (localisation des services), l'image...  

![nameRegion](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/vmNameRegionImage.png)  

Créer un compte admin (user name, password)  

![adminUserCreate](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/AdminUserCreate.png)  

Puis choisir les règles de port entrantes (HTTP/HTTPS/SSH)  

## Disques  

Choisir un type de disque système :  

![osDisk](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/diskOptions.png)  

Puis ajouter au moins 1 disque DATA :  

![dataDiskAdd](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/createDataLUN.png)  

![dataDiskOptions](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/createDataLUNOptions.png)  

## Réseau  
Choisir le "virtual network", le "subnet" et l ressource Azure "public ip" (faire "new" si pas de ressource déjà existante)  

![network1](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/networkInterface.png)  

Choisir quels ports seront autorisés au déploiement de la VM :  

