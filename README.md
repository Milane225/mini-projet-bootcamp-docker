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
