Pour changer le port 22 en 10022 :  
Editer le fichier /etc/ssh/sshd_config  
Retrouver la ligne qui contient "Port 22" (sous VIM, faire une recherche avec /)  
Enlever le # en début de ligne (il sert à "commenter" une ligne, elle ne sera donc pas prise en compte tant que "#" est là)  
Remplacer la ligne par "Port 10022"  

```console
groupe3@VMAdminB2G3:~$ cat /etc/ssh/sshd_config
#       $OpenBSD: sshd_config,v 1.103 2018/04/09 20:41:22 tj Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.

Include /etc/ssh/sshd_config.d/*.conf

Port 10022
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::
```  
Ensuite la machine sera normalement inaccessible tant que le port 10022 n'est pas autorisé via Azure.  Pour l'autoriser, il va falloir ajouter une règle dans la ressource "network security group" associée à la VM Admin :  

![resNSG]()  

Création de la règle :  

![creaRule1]()  
![creaRule2]()  
![creaRule3]()  


