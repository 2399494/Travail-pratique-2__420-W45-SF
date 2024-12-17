#### Nom du projet : 

#### Nom : Ait Oumasste  Tarik 

#### Date : 17-12-2024

#### Description du projet : 

## Section 1 : Vérification et conteneurs
## Étape 1: Vérification de l’installation
### Vérification de l'installation de Docker

Deux composantes ont été installées avec Docker :  
1. Docker Engine  
2. Docker Client

#### Les commandes de vérification
- Pour Docker client :
   ```
   docker --version
   ``` 
![description](Images/verif_Docker1.png). 

- Pour Docker Engine :
   ```
   docker info
   ```
![description](Images/verif_Docker2.png). 

## Étape 2: Création de conteneurs sur le poste local
#### Les commandes réalisées :
- Créer le réseau privé virtuel :

```
docker network create mon_reseau
```

résultat :
```
447cec546f8defccc9b22d369a1a5773f49fb1c618e5f87992ecb91ae522f4a4
```

- Lancer le conteneur Apache :
```
docker run -d --name apache --network mon_reseau -p 80:80 httpd:latest
```

résultat :
```
Unable to find image 'httpd:latest' locally
latest: Pulling from library/httpd
bc0965b23a04: Already exists 
d7ad38c6dd97: Pull complete 
4f4fb700ef54: Pull complete 
79b49624e34b: Pull complete 
7d9f97915db2: Pull complete 
9bd25d4f7b77: Pull complete 
Digest: sha256:f4c5139eda466e45814122d9bd8b886d8ef6877296126c09b76dbad72b03c336
Status: Downloaded newer image for httpd:latest
f67c4d46378478da157403df82e3b2bb6b3ca151abe3f308eab9d07d56cc82c6
```

- Lancer le conteneur MongoDB :
```
docker run -d --name mongodb --network mon_reseau -e MONGO_INITDB_ROOT_USERNAME=adminmongo MONGO_INITDB_ROOT_PASSWORD=EncoreUneAutreBD -v mongodb mongodb/mongodb-community-server
```

résultat :
```
Unable to find image 'mongodb/mongodb-community-server:latest' locally
latest: Pulling from mongodb/mongodb-community-server
6414378b6477: Pull complete 
10df5ab8c5b9: Pull complete 
eafb06b05f9b: Pull complete 
908826966c95: Pull complete 
365275fca898: Pull complete 
4b1e1c1ed576: Pull complete 
5d1410b7ae4c: Pull complete 
68449901ee70: Pull complete 
ba2ffdf84597: Pull complete 
4f4fb700ef54: Pull complete 
76a717ec5e23: Pull complete 
Digest: sha256:0bf4cc673f6a396bb1bfdb68dd5c3ef8a6deff92856abb966994add599d64440
Status: Downloaded newer image for mongodb/mongodb-community-server:latest
b6deee8ecd842283c590c8cce2e850463d0b7f59b197be71d11697e8a853096a
```

- Vérifier la présence des conteneurs :
```
docker ps
```

résultat :
```
CONTAINER ID   IMAGE                              COMMAND                  CREATED          STATUS          PORTS                               NAMES
b6deee8ecd84   mongodb/mongodb-community-server   "python3 /usr/local/…"   19 minutes ago   Up 19 minutes   27017/tcp                           mongodb
f67c4d463784   httpd:latest                       "httpd-foreground"       24 minutes ago   Up 24 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   apache
```

- Vérifier que les conteneurs sont bien reliés au réseau privé virtuel ```mon_reseau``` :
```
docker inspect apache mongodb  
```

-Vérifier les journaux apache :
```
docker logs apache
```
résultat :
```
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
[Tue Dec 17 18:52:38.950560 2024] [mpm_event:notice] [pid 1:tid 1] AH00489: Apache/2.4.62 (Unix) configured -- resuming normal operations
[Tue Dec 17 18:52:38.956497 2024] [core:notice] [pid 1:tid 1] AH00094: Command line: 'httpd -D FOREGROUND'
```

