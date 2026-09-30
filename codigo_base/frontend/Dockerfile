# =============================================================================
# Taller Evaluativo 2 - Fase 2: Empaquetamiento Inmutable Multi-Stage
# Frontend: studytrack-frontend
# =============================================================================

# ---------- Stage 1: Builder ----------
# TODO

# ---------- Stage 2: Runtime ----------
# TODO

#Stage 1: Builder 
FROM node:20-alpine AS builder

WORKDIR /app

# Copiar archivos de dependencias
COPY package*.json ./

# Instalar dependencias
RUN npm install

# Copiar código fuente
COPY . .

# Generar build de producción
RUN npm run build

# Stage 2: Runtime
FROM nginx:alpine

# Copiar el build generado por Vite
COPY --from=builder /app/dist /usr/share/nginx/html

# Copiar configuración personalizada de nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 3000

CMD ["nginx", "-g", "daemon off;"]