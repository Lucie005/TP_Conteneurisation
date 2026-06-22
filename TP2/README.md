# TP2 - Docker Compose : stack multi-services

Ce projet déploie une application découpée en services orchestrée avec Docker Compose.

## Architecture
* **Frontend** : Servi par Nginx, affiche une page web avec un formulaire. Accessible sur http://localhost:8080.
* **API** : API Node.js qui lit et écrit dans la base de données. Accessible sur http://localhost:3000.
* **Database** : Base de données PostgreSQL. Elle n'est pas accessible depuis l'extérieur, mais les données sont persistantes grâce à un volume nommé.
* **Adminer** : Interface web légère pour administrer la base de données. Accessible sur http://localhost:8081.

## Prérequis
Aucun mot de passe ne doit apparaître en clair. Créez un fichier `.env` local pour les secrets avec les variables suivantes :
```env
DB_NAME=tp2db
DB_USER=tp2user
DB_PASSWORD=votre_mot_de_passe
```

## Lancement
Construire et démarrer tous les services en arrière-plan :
```bash
docker compose up --build -d
```
Pour arrêter la stack sans perdre les données :
```bash
docker compose down
```