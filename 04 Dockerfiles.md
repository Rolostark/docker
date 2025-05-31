# 4. Sintaxis de Dockerfile y Buenas Prácticas (Multistage)

## ¿Qué aprenderás?
- Estructura de un Dockerfile.
- Buenas prácticas: imágenes multistage para optimizar tamaño y seguridad.
- Cómo construir y ejecutar imágenes y contenedores a partir de tu Dockerfile.

---

## 1. Sintaxis básica de un Dockerfile

Un Dockerfile define cómo se construye una imagen. Aquí tienes un ejemplo típico para una app Node.js:

```Dockerfile
# Dockerfile simple para Node.js
FROM node:18                 # 1. Imagen base oficial de Node.js
WORKDIR /app                 # 2. Carpeta de trabajo dentro del contenedor
COPY package*.json ./        # 3. Copia archivos de dependencias
RUN npm install              # 4. Instala dependencias
COPY . .                     # 5. Copia el resto del código fuente
CMD ["node", "index.js"]     # 6. Comando por defecto al iniciar el contenedor
```

**¿Qué hace cada instrucción?**

| Instrucción | Descripción                               | Ejemplo en el Dockerfile      |
|-------------|-------------------------------------------|------------------------------|
| `FROM`      | Define la imagen base                     | `FROM node:18`               |
| `WORKDIR`   | Carpeta de trabajo                        | `WORKDIR /app`               |
| `COPY`      | Copia archivos al contenedor              | `COPY . .`                   |
| `RUN`       | Ejecuta comandos durante la construcción  | `RUN npm install`            |
| `CMD`       | Comando por defecto al iniciar            | `CMD ["node", "index.js"]`   |

---

### 🚀 ¿Cómo construir y ejecutar tu imagen?

1. **Guarda el Dockerfile en tu proyecto**  
   Asegúrate de tener tu código fuente (por ejemplo, `index.js` y `package.json`) en la misma carpeta que tu `Dockerfile`.

2. **Construye la imagen Docker:**  
   Abre la terminal en la carpeta donde está tu Dockerfile y ejecuta:
   ```bash
   docker build -t mi-app-node .
   ```
   Esto crea una imagen llamada `mi-app-node`.

3. **Ejecuta un contenedor a partir de la imagen:**  
   ```bash
   docker run --rm -it -p 3000:3000 mi-app-node
   ```
   - `--rm` elimina el contenedor al salir.
   - `-it` te permite interactuar con el contenedor.
   - `-p 3000:3000` expone el puerto interno 3000 al 3000 de tu máquina (ajústalo según tu app).

---

## 2. Buenas prácticas: Multistage builds

Las **multistage builds** permiten crear imágenes finales más ligeras y seguras, ya que solo copian lo necesario para ejecutar la app.

**Ejemplo multistage para Node.js:**

```Dockerfile
# Etapa 1: Build
FROM node:18 AS build
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Etapa 2: Imagen final
FROM node:18-slim
WORKDIR /app
COPY --from=build /app/dist ./dist
CMD ["node", "dist/index.js"]
```

---

### 🚀 ¿Cómo construir y ejecutar una imagen multistage?

1. **Guarda el Dockerfile multistage en tu proyecto**  
   Asegúrate de tener tu código fuente y el script `npm run build` definido en tu `package.json`.

2. **Construye la imagen Docker:**  
   ```bash
   docker build -t mi-app-node-prod .
   ```
   Esto crea una imagen optimizada llamada `mi-app-node-prod`.

3. **Ejecuta el contenedor (ajusta puertos según tu app):**  
   ```bash
   docker run --rm -it -p 3000:3000 mi-app-node-prod
   ```

---

## Consejos adicionales de buenas prácticas

- **Usa `.dockerignore`** para evitar copiar archivos innecesarios.
- **Define variables de entorno** con `ENV` si es necesario.
- **No uses root:** especifica un usuario no root (`USER`) para mayor seguridad.
- **Agrupa comandos RUN** para reducir capas.
- **Prefiere imágenes oficiales y ligeras** (`-slim`, `-alpine`).

---

**¡Con esto podrás escribir, construir y ejecutar Dockerfiles eficientes y seguros para tus proyectos!**
