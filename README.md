# Déploiement de l'application **STUDENT_LIST** de l'entreprise POZOS
Il nous a été démandé pour ce projet de faire le déploiement de l'application dénommée **STUDENT_LIST** qui permettra à l'entreprise POZOS d'afficher la iste de leurs étudiants avec leurs âges.
L'application est composée de 2 modules interconntectés qui sont :
- Une API REST basée sur un fichier JSON qui renvoie la liste des étudiants demandée
- Une applation Web développée en HTML et PHP permettant à l'utilisateur final d'afficher la liste d'étudiants contenu dans le fichier JSON

## Objectifs du projet

- Créer un conteneur pour chaque module de l'application **STUDENT_LIST**
- Faire interagir les 2 modules
- Fournir un régistre privé

## Prérequis

Installation de docker sur la machine ou utilisation de dockerlabs.

## Structure du projet

```
mini-projet-bootcamp-docker/
├── simple_api                   
│   ├── Dockerfile               # Fichier permettant de construire l'image Doker de l'API
│   ├── requirements.txt         # 
│   ├── student_age.json         # Fichier au format JSON contenant le nom, prénom et l'âge des étudiants
│   ├── student_age.py           # Fichier contenant le code source de l'API en Python
│
├── Website                      # 
│   ├── index.php                # Page Web developpée en HTML/PHP qui consomme l'API qui affiche la liste des étudiants et leurs âges
│
├── Instructions.md              # Enoncé du projet
├── README.md                    # Documentation du projet
├── docker-compose-registry.yml  # pour lancer le registre local et son interface utilisateur
├── docker-compose.yml           # Permet de lancer l'API et l'application Web dans des conteneurs
````


## Déploiement

### Mise en place et test

#### 1- Clôner le repo
````
git clone https://github.com/diranetafen/student-list
````

#### 2- Construction de l'image Docker de l'API
==> Tout d'abord, se déplacer dans le repertoire contenant le fichier Dockerfile
````
cd mini-projet-bootcamp-docker/simple_api
````
==> Lancer la création de l'image
````
docker build . -t api_student_list:v1 .
````
==> Vérification de notre image créée
````
Docker images
````
<illustration en image>

#### 3- Création d'un réseau de type Bridge (Pont).C'est le réseau par défaut pour les conteneurs Docker qui leur permet de communiquer entre eux
==> Création du réseau Bridge
````
docker network create student_list_network --driver=bridge
````
==> Afficher la liste des réseaux
````
docker network ls
````
<illustration en image>


#### 4- Lancement du conteneur de l'API Backend avec une série de configurations spécifiques
==> Avant le lancement du conteneur, il faudrait se positionner à la racine du repertoire du projet
````
cd ..
````
==> Lancement du conteneur nommé api_student_list
````
docker run -d --name api_student_list --network student_list_network -v ./simple_api/:/data/ api_student_list
````
      Expliquation de la commande
      > **docker run** : commande principale pour lancer un conteneur basé sur une image
      > **-d** : lance le conteneur en mode détaché (exécution des tâches en arrière plan)
      > **--name api_student_list** : le nom du conteneur
      > **--network student_list_network** : connecte leconteneur au réseau Docker nommé student_list_network
      > **-v ./simple_api/:/data/** : cette option monte un volume entre la machine hôte et le conteneur
      > **api_student_list** : le nom de l'image utilisée pour créer le conteneur
==> Listons nos conteneurs en cours d'exécution parmi lesquels doit se trouver le conteneur api_student_list
````
docker ps
````
