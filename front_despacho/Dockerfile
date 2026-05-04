# --- ETAPA 1: Construcción (Builder) ---
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# --- ETAPA 2: Servidor Web de Producción ---
FROM nginx:alpine
# Copiamos el build optimizado de React/Vue al servidor Nginx
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]