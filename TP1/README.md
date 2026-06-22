# TP1 - Réparation d'une image Docker

Ce dossier contient la correction du Dockerfile initial pour conteneuriser une petite application Node.js, en respectant les bonnes pratiques de production et de sécurité.

## Améliorations apportées
* **Réduction de la taille** : L'image finale est inférieure à 200 MB.
* **Sécurité** : 
  * Aucun secret n'est présent dans l'image.
  * Le container ne tourne pas en root. L'utilisateur `node` est utilisé.
* **Optimisation du cache** : Le cache Docker est exploité correctement en copiant le fichier package.json avant le code source.
* **Propreté** : Seuls les outils strictement nécessaires sont présents et un fichier `.dockerignore` a été ajouté pour ne pas envoyer les fichiers inutiles dans le contexte de build.

## Lancement

1. Builder l'image corrigée :
   ```bash
   docker build -t tp1:corrige .
   ```
2. Lancer le container :
   ```bash
   docker run --rm -p 3000:3000 tp1:corrige
   ```
3. L'application reste accessible sur le port 3000. Ouvrir `http://localhost:3000`.