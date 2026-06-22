# 1- Diagnostic :

## Sans modifier quoi que ce soit, identifiez tous les problèmes dans le Dockerfile.

Pour chaque problème trouvé, répondez à ces 3 questions :
1.	Quelle ligne est en cause ?
2.	Quel est le problème exact ?
3.	Quelle est la conséquence en production ?

1er problème :

    lignes 5 à 7 : Les secrets (API_KEY, DB_PASSWORD) sont écrits en dur avec ENV.
        -> Conséquence en prod : Toute personne ayant accès à l'image peut lire les mots de passe de production via un docker inspect.
        -> Correction : Supprimer ces variables du Dockerfile et les passer au runtime (ex: via un fichier .env).

2ème problème :

    lignes 10 à 14 : Le COPY . . est fait avant le RUN npm install.
        -> Conséquence en prod : La moindre modification d'un fichier source invalide le cache Docker pour l'étape d'installation, ralentissant considérablement le build.
        -> Correction : Copier uniquement package*.json, lancer npm install, puis copier le reste du code.

3ème problème :

    Le container s'exécute avec l'utilisateur root par défaut.
        -> Conséquence en prod : Si l'application est compromise, l'attaquant obtient les droits administrateur sur le container.
        -> Correction : Utiliser l'instruction USER node (l'utilisateur non-root inclus dans les images Node).

4ème problème :

    lignes 18 à 24 : Installation de paquets systèmes inutiles (curl, vim, git, etc.) avec apt-get.
        -> Conséquence en prod : L'image finale est alourdie inutilement et la surface d'attaque est augmentée.
        -> Correction : Supprimer complètement ce bloc d'installation.

5ème problème :

    lignes 1 : Utilisation de l'image de base complète FROM node:18.
        -> Conséquence en prod : L'image de base est très lourde (souvent > 900 MB), ce qui empêche d'atteindre l'objectif de taille.
        -> Correction : Remplacer par une version allégée comme FROM node:18-alpine.