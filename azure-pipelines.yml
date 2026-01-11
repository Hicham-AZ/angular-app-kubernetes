# --------------------
# Stage 1 - Build
# --------------------
FROM node:18-alpine AS builder

# Crée le répertoire de travail
WORKDIR /app

# Copie package.json et package-lock.json pour installer les dépendances
COPY package*.json ./

# Installe les dépendances
RUN npm install

# Copie tout le code source
COPY . .

# Build de l’application (Angular / Node)
RUN npm run build --prod

# --------------------
# Stage 2 - Production
# --------------------
FROM nginx:alpine

# Supprime le default.conf de nginx
RUN rm -rf /etc/nginx/conf.d/default.conf

# Copie le fichier de configuration nginx (si tu en as un)
# COPY nginx.conf /etc/nginx/conf.d

# Copie les fichiers build du stage précédent
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose le port
EXPOSE 80

# Commande par défaut
CMD ["nginx", "-g", "daemon off;"]
