# Dependecias de desarrollo
FROM node:19.2-alpine3.16 AS deps
WORKDIR /app
COPY  package.json ./
RUN npm install

# Build & Test
FROM node:19.2-alpine3.16 AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run test

# Dependencias de Producción
FROM node:19.2-alpine3.16 AS prod-deps
WORKDIR /app
COPY  package.json ./
RUN npm install --prod

# Ejecutar la App
FROM node:19.2-alpine3.16 AS runner
WORKDIR /app
COPY --from=prod-deps /app/node_modules ./node_modules
COPY app.js ./
COPY tasks/ ./tasks
CMD [ "node", "app.js" ]