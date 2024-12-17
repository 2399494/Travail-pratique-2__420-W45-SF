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
Créer le réseau privé virtuel :
```
docker network create mon_reseau
```

Lancer le conteneur Apache :
```
docker run -d --name apache --network mon_reseau -p 80:80 httpd:latest
```

Lancer le conteneur MongoDB :
```
docker run -d --name mongodbr --network mon_reseau -e MONGO_INITDB_ROOT_USERNAME=adminmongo MONGO_INITDB_ROOT_PASSWORD=EncoreUneAutreBD -v mongodb mongodb/mongodb-community-server
```
