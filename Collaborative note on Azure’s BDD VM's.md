# Collaborative creation of Nextcloud VMs

## ***0 - Sommaire<a name="home"></a>

***[1 - Plan d'action](#Actplan)***

***[2 - Topogragie du réseau sur Azure en Flowchart](#NetFlo)***


## ***1 - Plan d'action :<a name="Actplan"></a>***

        - Tâches à faire  
 
        - crée le schéma réseau 

        - Créer 3 VMs pour NextCloud  

        - Déployer les VMs NextCloud 
 
        - Configurer les VM sur les mêmes réseaux
 
        - Créer les utilisateurs et accorder les droits d’accès
 
        - Tester la structure 
 
        - Création des différentes documentations


[Retour au sommaire](#home)



## ***2 - Topogragie du réseau sur Azure en Flowchart***<a name="NetFlo"></a>

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


***3 - Liste des resources Azure prévues à déployer***<a name=List></a>

    - 3 VM Ubuntu 20
          - 2 VM avec 64Gb Standard SDD - Dual Core - 8Gb RAM
          - 1 VM avec 128Gb Premium SSD - Dual Core - 16Gb RAM
    - 1 virtual network
    - 1 virtual gateway
    - 3 public IP adresses (1 temporary)
    - 1 Azure Sentry
    - 









