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

- Un cluster Kubernetes fonctionnel (dockerlabs, Minikube ou un cluster cloud).
- `kubectl` installé et configuré pour interagir avec votre cluster.
- Accès à une image Docker de WordPress et de MySQL sur un registre public ou privé.

## Structure du projet

```
mini-projet-bootcamp-kubernetes/
├── deployment-mysql.yml             # Deployment MySQL
├── deployment-wordpress.yml         # Deployment WordPress
├── namespace.yml                    # Création du NameSpace
├── pv.yml                           # Provisionnement du PersistentVolume (PV)
├── pvc.yml                          # Association du PersistentVolume (PV) au PersistentVolumeClaims (PVC)
├── service-cluster-ip-mysql.yml     # Service MySQL (ClusterIP)
├── service-nodeport-wordpress.yml   # Service WordPress (NodePort)
├── README.md                        # Documentation du projet
````


## Déploiement
