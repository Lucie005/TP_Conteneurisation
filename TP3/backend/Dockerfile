FROM node:20-alpine

WORKDIR /app

# Optimisation du cache pour les dépendances
COPY package*.json ./
RUN npm install

# Copie du code source
COPY . .

EXPOSE 3001

# Commande de démarrage générique
CMD ["npm", "start"]