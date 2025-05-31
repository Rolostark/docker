# 4. Sintaxis (FROM, RUN, COPY, CMD, etc.), Buenas prácticas (multistage)

## ¿Qué aprenderás?
- Estructura de un Dockerfile.
- Buenas prácticas: imágenes multistage.

---

### Paso 1: Sintaxis básica de un Dockerfile

```Dockerfile
# Dockerfile simple para Node.js
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "index.js"]
```

- **FROM:** Imagen base.
- **WORKDIR:** Carpeta de trabajo.
- **COPY:** Copia archivos.
- **RUN:** Ejecuta comandos.
- **CMD:** Comando por defecto.

---

### Paso 2: Multistage builds

Reduce el tamaño de la imagen final:

```Dockerfile
# Dockerfile multistage para Node.js
FROM node:18 AS build
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM node:18-slim
WORKDIR /app
COPY --from=build /app/dist ./dist
CMD ["node", "dist/index.js"]
```