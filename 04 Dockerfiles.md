# 4. Sintaxis de Dockerfile y Buenas Prácticas (Multistage) con el Proyecto `mi-proyecto-app`

## ¿Qué aprenderás?
- Estructura de un Dockerfile usando tu proyecto real.
- Buenas prácticas: imágenes multistage para optimizar tamaño y seguridad.
- Cómo construir y ejecutar imágenes y contenedores de **mi-proyecto-app** desde cero.

---

## ¿Qué es un multistage build en Docker?

Un **multistage build** es una técnica para crear imágenes Docker más ligeras y seguras. Permite usar varias etapas (stages) en un solo Dockerfile, donde cada etapa puede tener su propia imagen base y propósito. Solo los archivos necesarios de las etapas previas se copian a la imagen final, lo que minimiza el tamaño y los archivos innecesarios.

### ¿Por qué usar multistage?
- **Reduce el tamaño de la imagen final:** Solo incluye lo necesario para ejecutar tu app, dejando fuera dependencias de desarrollo y archivos temporales.
- **Mejora la seguridad:** Menos archivos y herramientas innecesarias significa menos superficie de ataque.
- **Mantiene el Dockerfile simple:** No necesitas scripts adicionales ni varios Dockerfile para dev/prod.

---

## 1. Estructura ejemplo del proyecto `mi-proyecto-app`

Supón que tu app es una aplicación Node.js sencilla. La estructura sería:

```
mi-proyecto-app/
├── Dockerfile
├── .dockerignore
├── package.json
├── package-lock.json
├── index.js
├── /dist       # (solo si usas build, por ejemplo con TypeScript o bundlers)
└── ... (otros archivos)
```

### Ejemplo de archivos esenciales

**index.js**
```js
// index.js
console.log('¡Hola desde mi-proyecto-app!');
```

**package.json**
```json
{
  "name": "mi-proyecto-app",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "build": "echo 'No hay build en este ejemplo simple'"
  }
}
```

**.dockerignore**
```
node_modules
npm-debug.log
dist
.git
```

---

## 2. Dockerfile básico para `mi-proyecto-app`

```Dockerfile
# Dockerfile simple para mi-proyecto-app
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "start"]
```

---

### 🚀 ¿Cómo construir y ejecutar tu proyecto con Docker?

1. **Ubícate en la raíz del proyecto:**
   ```bash
   cd ruta/a/mi-proyecto-app
   ```

2. **Construye la imagen Docker:**
   ```bash
   docker build -t mi-proyecto-app .
   ```

3. **Ejecuta un contenedor con tu imagen:**
   ```bash
   docker run --rm -it mi-proyecto-app
   ```

   Si tu app expone puertos, usa por ejemplo:  
   ```bash
   docker run --rm -it -p 3000:3000 mi-proyecto-app
   ```

---

## 3. Dockerfile multistage build (opcional, para proyectos con build)

Si tu proyecto requiere un paso de build (por ejemplo, usa TypeScript o Webpack):

```Dockerfile
# Dockerfile multistage para mi-proyecto-app
FROM node:18 AS build
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM node:18-slim
WORKDIR /app
COPY --from=build /app/dist ./dist
CMD ["node", "dist/index.js"]
```

### Explicación de cada etapa:

1. **Etapa de build**  
   - Utiliza Node completo.
   - Instala dependencias y ejecuta el build.
   - Genera los archivos de salida en `/app/dist`.

2. **Etapa final**  
   - Usa una imagen más ligera (`node:18-slim`).
   - Solo copia el resultado del build (`/app/dist`).
   - Ejecuta el archivo principal desde esa carpeta.

Visualmente:

```
+-------------------------+
| 1. Build Stage          |  (Node completo, dependencias dev, src, tools)
+-------------------------+
| npm install             |
| npm run build           |
| /app/src                |
| /app/dist (generado)    |
+-------------------------+
            |
            |   COPY --from=build /app/dist ./dist
            v
+-------------------------+
| 2. Final Stage          |  (Node slim, solo /dist)
+-------------------------+
| /app/dist               |
| node dist/index.js      |
+-------------------------+
```

Asegúrate de que tu script de build genere los archivos en `/dist`.

---

### 🚀 ¿Cómo construir y ejecutar con multistage?

1. **Construye la imagen optimizada:**
   ```bash
   docker build -t mi-proyecto-app:prod .
   ```

2. **Ejecuta el contenedor de producción:**
   ```bash
   docker run --rm -it -p 3000:3000 mi-proyecto-app:prod
   ```

---

## 4. Buenas prácticas

- Usa `.dockerignore` para evitar copiar archivos innecesarios.
- Siempre revisa los logs con `docker logs <container_id>` si hay problemas.
- Personaliza puertos y nombres según tu app.
- Mantén tu Dockerfile lo más simple y claro posible.
- Si no tienes build, usa el Dockerfile simple; si tienes build (TypeScript, bundlers), usa multistage.

---

**¡Así puedes dockerizar, construir y ejecutar el proyecto `mi-proyecto-app` de principio a fin, aplicando buenas prácticas y obteniendo imágenes ligeras con multistage!**
