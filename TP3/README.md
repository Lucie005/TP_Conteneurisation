# TP3 - Conteneurisation de TaskFlow

L'objectif de ce projet est de conteneuriser l'application de gestion de tâches TaskFlow.

## Services de la stack
* **Frontend** : Utilise l'image `nginx:alpine` pour servir l'interface web statique sur le port 80.
* **Backend** : Utilise l'image `node:20-alpine` pour l'API REST.
* **Cache** : Utilise l'image `redis:7-alpine`. Il n'est pas accessible depuis l'extérieur, seul le backend peut le joindre. Un volume nommé est déclaré pour conserver ses données.

## Configuration
Le fichier `docker-compose.yml` s'appuie sur des variables d'environnement. Un fichier `.env.example` sert de modèle pour les variables nécessaires, sans vraie valeur sensible. 
Copiez-le pour créer votre configuration locale :
```bash
cp .env.example .env
```

## Lancement
Aucune installation de Node, Redis ou Nginx n'est nécessaire sur la machine. Une seule commande permet de builder et lancer toute l'application depuis la racine :
```bash
docker compose up --build
```