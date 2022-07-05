# Collaborative creation of Nextcloud VMs

    Demande utilisateur :

    Dans le cadre du projet “LifeSense”, nous avons besoin d’échanger des gros fichiers (plusieurs GO). Nous souhaitons le faire sans 
    passer par un drive tierce, de façon simple par un navigateur web, avec des accès sécurisés par utilisateur.

## ***Sommaire<a name="home"></a>***

***[1 - Topographie du réseau sur Azure en Flowchart](#NetFlo)*** 

***[2 - Ressources nécessaires prévues](#Res)***

***[3 - Plan d'action](#Actplan)***

## ***1 - Topographie du réseau sur Azure en Flowchart***<a name="NetFlo"></a>

```mermaid
flowchart TD

    subgraph rg1 [Azure Ressource Group]
        
        subgraph use [usage]

        subgraph bdd1 [BDD]
            priv_1[Private Network card]
            virt_1[Fast Virtual Disk]
            os_1{OS}
        end
        
        subgraph app1 [Appli]
            priv_2[Private Network card]
            pub_2[Public Network card]
            virt_2[Slow Virtual Disk]
            os_2{OS}
        end

        end

        subgraph  admin1 [Bouncer]
            priv_3[Private Network card]
            pub_3[Public Network card]
            virt_3[Slow Virtual Disk]
            os_3{os}
        end

        gw(gateway)
        sentry[Azure Sentry]

        

    end
    
    subgraph outside[outside]
        usr[user]
        admin[Administrateur]
        web{internet}
    end

    usr <-->|http only| web
    admin <-.->|SSH| web
    
    web <-->|User HTTP/S| gw
    web <-.->|admin SSH| gw
    
    gw <-->|User HTTP only| pub_2
    gw <-.->|admin SSH| pub_3
    sentry <--> priv_1 & priv_2 & priv_3
    
    os_1 <--> virt_1
    os_1 <--> priv_1
    
    os_2 <--> virt_2
    os_2 <--> priv_2
    os_2 <--> pub_2

    os_3 <--> virt_3
    os_3 <--> priv_3
    os_3 <--> pub_3

    priv_1 <--> priv_2
    priv_3 <-.-> priv_1 & priv_2
    

    classDef sec fill:#faa,stroke:#f66,stroke-width:4px,color:#fff,stroke-dasharray: 5 5;
    class admin,admin1,bdd1, sec;
    classDef prim fill:#aff,stroke:#025,stroke-width:2px,color:#003;
    class usr,app1, prim;



```

[Retour au sommaire](#home)


## ***2 - Liste des ressources Azure prévues à déployer***<a name=Res></a>

    - 3 VM Ubuntu 20
          - 2 VM avec 64Gb Standard SDD - Dual Core - 8Gb RAM
            - 1 VM d'Administration "rebond" pour accéder aux 2 autres en SSH
          - 1 VM avec 128Gb Premium SSD - Dual Core - 16Gb RAM
            - VM de Base de Donnée en MariaBD
    - 1 virtual network
    - 1 virtual gateway
    - 3 adresses IP publiques (1 temporaire)
    - 1 Azure Sentinel  

[Retour au sommaire](#home)

## ***3 - Plan d'action :<a name="Actplan"></a>***

        - Planifier les actions et quelles ressources mettre en place
 
        - Créer le schéma réseau

        - Créer 3 VMs pour NextCloud
            - 1 VM Admin
            - 1 VM BDD
            - 1 VM Applicative

        - Déployer NextCloud sur la VM Applicative, MariaDB sur la VM BDD

        - Créer les utilisateurs/groupes et accorder les droits d’accès

        - Création des clés SSH pour les différents Users

        - Configurer les accès au réseau des VMs
            - Modifier les ports d'accès (10022 au lieu de 22/ 10080 au lieu de 80...)
            - Couper l'accès SSH public aux VMs Appli et BDD
 
        - Tester la structure
            - Accès au portail web NextCloud en tant que "user" (http/10080)
            - Vérification du logging d'Azure Sentinel
            - Test de disponibilité Application Insights

        - Accès à l'application via TLS (HTTPS)

        - Création des différentes documentations


[Retour au sommaire](#home)







