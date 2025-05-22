# Utiliser l'image officielle Node.js pour le développement
FROM node:18 AS development

# Définir le répertoire de travail à l'intérieur du conteneur
WORKDIR /usr/src/app

# Copier tout le code source dans le conteneur
COPY package*.json ./

# Installer les dépendances Angular
RUN npm install

# Copier tout le reste du code source
COPY . .

# Exposer le port utilisé par le serveur de développement Angular
EXPOSE 4200

# Commande pour démarrer le serveur Angular en mode développement
CMD ["npm", "start"]

# Utiliser l'image officielle Node.js comme étape de build
FROM node:18 AS production


# Définir le répertoire de travail
WORKDIR /app

COPY . .

RUN npm install

RUN npm run build -- --configuration build

# Utiliser une image Nginx pour servir l'application Angular
FROM nginx:alpine

COPY --from=production /app/dist/ /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf

# Exposer le port 80 pour Nginx
EXPOSE 80

# Démarrer Nginx
CMD ["nginx", "-g", "daemon off;"]
