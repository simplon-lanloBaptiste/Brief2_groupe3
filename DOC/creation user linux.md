Création du user :  
```console
sudo useradd -m -d /home/alain alain
```

Pour ajouter le user aux mêmes groupes que notre utilisateur administrateur j'ai créé une boucle qui liste les groupes en question et ajoute l'utilisateur à chacun de ces groupes :  

```console
for groupe in `cat /etc/group | grep -i groupe3 | awk -F ':' '{print $1}'`;do usermod -a -G ${groupe} alain;done;
```

Pour pouvoir activer la clé ssh :  
Créer un répertoire .ssh dans le home  
```console
sudo mkdir ~/.ssh  
```

Changer le propriétaire du répertoire /home/[utilisateur]/.ssh

```console
sudo chown $USER:$USER ~/.ssh -R
chmod 700 /home/alain/.ssh  
chmod 600 /home/alain/.ssh/authorized_keys  
```

Ensuite, soit : créer un fichier authorized_keys (commande touch), soit : dans notre cas, j'ai récupéré celui du premier user que nous avions créé :  
```console
cp /home/groupe3/.ssh/* /home/alain/.ssh/
```

Le fichier contient déjà la clé publique associée à l'hôte utilisé pour la connexion en ssh  
relancer le daemon ssh :  

```console
sudo service ssh restart
```

Désormais le user "alain" peut se connecter via la clé ssh sur la vm Admin  
