# --- ETAPA 1: Compilación ---
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# --- ETAPA 2: Producción ---
FROM nginx:1.25-alpine
# Copiamos el build estático al directorio de Nginx
COPY --from=builder /app/dist /usr/share/nginx/html
# Copiamos una configuración básica para manejar rutas de React si es necesario
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]