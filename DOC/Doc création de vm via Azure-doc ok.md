# Création d'une VM via le portail Azure


## 1. Informations basiques  
___
All resources > Create > Virtual machine  

![creating a vm](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/creating%20a%20VM.png)  

Choisir "subscription" et "resource group"  

![subres](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/subres.png)  

Choisir un nom pour la VM, la "Region" (localisation des services), l'image...  

![nameRegion](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/vmNameRegionImage.png)  

Créer un compte admin (user name, password)  

![adminUserCreate](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/AdminUserCreate.png)  

Puis choisir les règles de port entrantes (HTTP/HTTPS/SSH)  

## 2. Disques  
___
Choisir un type de disque système :  

![osDisk](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/diskOptions.png)  

Puis ajouter au moins 1 disque DATA :  

![dataDiskAdd](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/createDataLUN.png)  

![dataDiskOptions](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/createDataLUNOptions.png)  

## 3. Réseau  
___
Choisir le "virtual network", le "subnet" et l ressource Azure "public ip" (faire "new" si pas de ressource déjà existante)  

![network1](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/networkInterface.png)  

Choisir quels ports entrants seront autorisés au déploiement de la VM :  

![networkPorts](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/networkSelectPorts.png)  

## 4. Création de la VM
___
Si tout est conforme, passer à "review and create", un résumé du produit et du prix est visible (voir screenshot), et toutes les informations relatives à la VM sont résumées plus bas dans la page du portail Azure  

![createVM](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/vmReviewAndCreate.png)  

## 5. Vérification des ressources  
___
Si tout s'est bien déroulé, nous allons pouvoir retrouver la vm et les ressources automatiquement créées dans "all resources", en filtrant sur notre "resource group" :  

![filterResGrp](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/filterResourceGroups.png)  

![allResourcesVm](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/allResourcesGrp3.png)  

Exemple :  

| NAME | TYPE | RESOURCE GROUP | LOCATION | SUBSCRIPTION |
| --- | --- | --- | --- | --- |
| VMAdminB2G3 | Virtual machine | brief_2_groupe_3 | West US 3 | Simplon OCC Montpellier ADMIN CLOUD |
| VMAppliB2G3 | Virtual machine | brief_2_groupe_3 | West US 3 | Simplon OCC Montpellier ADMIN CLOUD |

[Lien vers l'extract en .csv](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/DOC/AzureresourcesBrief2.csv)  
