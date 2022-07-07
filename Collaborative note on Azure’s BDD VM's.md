# Collaborative creation of Nextcloud VMs

    Demande utilisateur :

    Dans le cadre du projet “LifeSense”, nous avons besoin d’échanger des gros fichiers (plusieurs GO). Nous souhaitons le faire sans 
    passer par un drive tierce, de façon simple par un navigateur web, avec des accès sécurisés par utilisateur.

## ***Sommaire<a name="home"></a>***

***[1 - Topologie du réseau sur Azure en Flowchart](#NetFlo)*** 

***[2 - Ressources nécessaires prévues](#Res)***

***[3 - Plan d'action](#Actplan)***

***[4 - Création d'une VM via le portail Azure](#Crea)***

***[X - Commandes prévues](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/Commandes%20pr%C3%A9vues)***

## ***1 - Topologie du réseau sur Azure en Flowchart***<a name="NetFlo"></a>

```mermaid
flowchart TD

    subgraph rg1 [Azure Ressource Group <br> Local network <br> 10.0.3.0/24]
        
        subgraph use [usage]

            subgraph bdd1 [BDD]
                priv_1[Private Network card]
                virt_1[Premium SSD]
            end
        
            subgraph app1 [Appli]
                priv_2[Private Network card]
                pub_2[Public Network card]
                virt_2[Large SSD]
            end

        end

        subgraph  admin1 [Bouncer]
            priv_3[Private Network card]
            pub_3[Public Network card]
            virt_3[Standard HDD]
        end

        gw(gateway)
        sentry[Azure Sentinel]

    end
    
    subgraph outside[outside]
        usr[user]
        admin[Administrateur]
        web{internet}
    end

    usr <-->|http only| web
    admin <-.->|admin SSH| web
    
    web <-->|User HTTP/S| gw
    web <-.->|admin SSH| gw
    
    gw <-->|User HTTP only <br> 10.0.3.0/24|pub_2
    gw <-.->|admin SSH <br> 10.0.3.0/24|pub_3

    sentry <-.->|via 10.0.3.0/24| priv_1 & priv_2 & priv_3

    priv_1 <-->|SQL via <br> 10.0.3.0/24| priv_2
    priv_3 <-.->|ssh via <br> 10.0.3.0/24| priv_1
    priv_3 <-.->|ssh via <br> 10.0.3.0/24| priv_2

    classDef sec fill:#faa,stroke:#f66,stroke-width:4px,color:#fff,stroke-dasharray: 5 5;
    class admin,admin1,bdd1, sec;
    classDef prim fill:#aff,stroke:#025,stroke-width:2px,color:#003;
    class usr,app1, prim;

```

[Retour au sommaire](#home)


## ***2 - Liste des ressources Azure prévues à déployer***<a name=Res></a>

    - 3 VM Ubuntu 20
            - 1 VM Admin bastion pour accès SSH aux autres VMs avec
                - 1vCPU
                - 3.5Gb RAM
                - 1 disque OS 30Gb standard HDD
                - 1 disque data 32Gb standard HDD
            - 1 VM Appli avec 
                - 2vCPU
                - 8Gb RAM
                - 1 disque OS 30Gb standard HDD
                - 1 disque data 256Gb Premium SSD
            - 1 VM de Base de Donnée en MariaBD avec
                - 2vCPU
                - 16Gb RAM
                - 1 disque OS 30Gb standard HDD
                - 1 disque data 32Gb standard SSD
    - 1 virtual network
        - masque de sous réseau 10.0.3.0/24
    - 1 virtual gateway
    - 3 adresses IP publiques (1 temporaire), cf table ip ci dessous
    - 1 Azure Sentinel  

Table d'adressage IP :  

| VM | Private IP | Public IP |
| :--- | :---: | ---: |
| Admin | 10.0.3.4 | 20.150.147.129 |
| Appli | 10.0.3.5 | 20.118.188.191 |
| BDD | 10.0.3.6 | 20.125.132.145 |

[Retour au sommaire](#home)

## ***3 - Plan d'action :<a name="Actplan"></a>***

- [x] Planifier les actions et quelles ressources mettre en place
 
- [x] Créer le schéma réseau

        - Création des clés SSH

        - Créer 3 VMs pour NextCloud
            - 1 VM Admin
            - 1 VM BDD
            - 1 VM Applicative

        - Configurer les accès au réseau des VMs
            - Modifier les ports d'accès (10022 au lieu de 22/ 10080 au lieu de 80...)
            - Couper l'accès SSH public aux VMs Appli et BDD

        - Installation des prérequis (PHP, Apache)
        Créer une base de données MariaDB sur la VM BDD
        Déployer NextCloud sur la VM Applicative

        - Créer les utilisateurs/groupes et accorder les droits d’accès
 
        - Tester la structure
            - Accès au portail web NextCloud en tant que "user" (http/10080)
            - Vérification du logging d'Azure Sentinel
            - Test de disponibilité Application Insights

        - Accès à l'application via TLS (HTTPS)

        - Création des différentes documentations

        - Répondre au client


Commentaire : représenter le réseau à déployer sous forme de tableau (adressages IPs, ports, etc)

[Retour au sommaire](#home)


## ***4 - Création d'une VM via le portail Azure<a name="Crea"></a>***


### ***4-1. Informations basiques***
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

### ***4-2. Disques***
___
Choisir un type de disque système :  

![osDisk](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/diskOptions.png)  

Puis ajouter au moins 1 disque DATA :  

![dataDiskAdd](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/createDataLUN.png)  

![dataDiskOptions](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/createDataLUNOptions.png)  

### ***4-3. Réseau***
___
Choisir le "virtual network", le "subnet" et l ressource Azure "public ip" (faire "new" si pas de ressource déjà existante)  

![network1](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/networkInterface.png)  

Choisir quels ports entrants seront autorisés au déploiement de la VM :  

![networkPorts](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/networkSelectPorts.png)  

### ***4-4. Création de la VM***
___
Si tout est conforme, passer à "review and create", un résumé du produit et du prix est visible (voir screenshot), et toutes les informations relatives à la VM sont résumées plus bas dans la page du portail Azure  

![createVM](https://github.com/simplon-lanloBaptiste/Brief2_groupe3/blob/main/IMG/vmReviewAndCreate.png)  

### ***4-5. Vérification des ressources***
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


[Retour au sommaire](#home)


