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
├── simple_api                   # Deployment MySQL
│   ├── Dockerfile               # Deployment WordPress
│   ├── student_age.json         # Deployment WordPress
│   ├── student_age.py           # Deployment WordPress
│
├── Website                      # Création du NameSpace
│   ├── index.php                # Deployment WordPress
│
├── Instructions.md              # Enoncé du projet
├── README.md                    # Documentation du projet
├── docker-compose-registry.yml  #
├── docker-compose.yml           #
````


## Déploiement
