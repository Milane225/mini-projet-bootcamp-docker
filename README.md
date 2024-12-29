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
│   ├── index.php                # Page Web developpée en HTML/PHP qui consomme l'API et affiche la liste des étudiants et leurs âges
│
├── Instructions.md              # Enoncé du projet
├── README.md                    # Documentation du projet
├── docker-compose-registry.yml  # pour lancer le registre local et son interface utilisateur
├── docker-compose.yml           # Permet de lancer l'API et l'application Web dans des conteneurs
````


## Déploiement avec la ligne de commande

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
   **Expliquation de la commanden** :<br>
    > **docker run** : commande principale pour lancer un conteneur basé sur une image<br>
    > **-d** : lance le conteneur en mode détaché (exécution des tâches en arrière plan)<br>
    > **--name api_student_list** : le nom du conteneur<br>
    > **--network student_list_network** : connecte leconteneur au réseau Docker nommé student_list_network<br>
    > **-v ./simple_api/:/data/** : cette option monte un volume entre la machine hôte et le conteneur<br>
    > **api_student_list** : le nom de l'image utilisée pour créer le conteneur<br>
    
==> Listons nos conteneurs en cours d'exécution parmi lesquels doit se trouver le conteneur api_student_list
````
docker ps
````

#### 5- Mise à jour du fichier inex.html contenu dans le dossier website
==> Ligne du fichier à mettre à jour <br>
`$url = 'http://<api_ip_or_name:port>/pozos/api/v1.0/get_student_ages'`

==> La remplacer par la ligne qui suit <br>
````
http://api_student_list:5000/pozos/api/v1.0/get_student_ages
````

#### 6- Lancement du conteneur de l'application Web
==> Lancement du conteneur
````
docker run -d --name=webapp_student_list -p 80:80 --network=student_list_network -v ./website/:/var/www/html -e USERNAME=toto -e PASSWORD=python php:apache
docker ps
````

==>Les valeurs saisies pour les variables d'environnements `-e USERNAME=toto` et `-e PASSWORD=python` sont contenus dans le fichier `.simple_api/student_age.py`

#### 7- Teste de l'API via l'application Web

##### 7-a) Teste avec la ligne de commande
==> Lancement du test avec la ligne de commande
docker exec webapp_student_list curl -u toto:python -X GET http://api_student_list:5000/pozos/api/v1.0/get_student_ages
==> Résultat du test de la ligne de commande

##### 7-b) Teste sur un navigateur Web
==> Teste sur dockerlabs

==>Teste sur vagrant
   - Récuperer l'adresse IP de votre machine avec la commande qui suit
     ``hostname -I``
   - Renseigner l'adresse IP de votre machine et le port exposé dans le navigateur
     ``192.168.5.2:80``

#### 8- Suppression de notre environnement de travail
````
docker stop api.student_list
docker stop webapp.student_list
docker network rm student_list.network
docker network ls
docker ps
````

## Déploiement avec l'Infastructure as Code (IaC)
L'IaC nous permet d'automatiser le déploiement de de nos conteneurs dans un fichier YML. Cela nous évite de faire nos déploiement manuellement comme cela a été le cas jusqu'à présent.

#### 1- Utilisation du fichier docker-compose pour le déploiement de nos services et réseaux
````
docker-compose up -d
````

