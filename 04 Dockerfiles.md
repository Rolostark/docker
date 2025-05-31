# 4. Sintaxis de Dockerfile y Buenas Prácticas (Multistage) con el Proyecto `mi-proyecto-app`

## ¿Qué aprenderás?
- Estructura de un Dockerfile usando tu proyecto real.
- Buenas prácticas: imágenes multistage para optimizar tamaño y seguridad.
- Cómo construir y ejecutar imágenes y contenedores de **mi-proyecto-app**.

---

## 1. Sintaxis básica de un Dockerfile

Un Dockerfile define cómo se construye una imagen. Por ejemplo, para tu app Node.js:

```Dockerfile
# Dockerfile simple para mi-proyecto-app
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "index.js"]
```

**¿Para qué sirve cada instrucción?**

| Instrucción | Descripción                               |
|-------------|-------------------------------------------|
| `FROM`      | Imagen base (Node.js 18)                  |
| `WORKDIR`   | Carpeta de trabajo dentro del contenedor  |
| `COPY`      | Copia archivos desde tu proyecto real     |
| `RUN`       | Ejecuta comandos durante el build         |
| `CMD`       | Comando por defecto al iniciar el contenedor |

---

### 🚀 ¿Cómo construir y ejecutar `mi-proyecto-app`?

1. **Ubícate en la raíz del proyecto (donde está tu Dockerfile):**
   ```bash
   cd ruta/a/mi-proyecto-app
   ```

2. **Construye la imagen Docker:**
   ```bash
   docker build -t mi-proyecto-app .
   ```

3. **Ejecuta un contenedor con tu imagen:**
   ```bash
   docker run --rm -it -p 3000:3000 mi-proyecto-app
   ```
   Ajusta el puerto según el que use tu proyecto.

---

## 2. Buenas prácticas: Multistage builds

Las **multistage builds** permiten crear imágenes finales más ligeras, copiando solo lo necesario para ejecutar la app.

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

---

### 🚀 Ejecución paso a paso con multistage

1. **Construye tu imagen optimizada:**
   ```bash
   docker build -t mi-proyecto-app:prod .
   ```

2. **Ejecuta el contenedor de producción:**
   ```bash
   docker run --rm -it -p 3000:3000 mi-proyecto-app:prod
   ```

---

## Consejos adicionales

- **Usa un archivo `.dockerignore`** para evitar copiar archivos innecesarios (por ejemplo, `node_modules`, `.git`, etc.).
- **Verifica que tengas scripts de build en tu `package.json`** si usas multistage (`npm run build`).
- **Personaliza el puerto expuesto** en el comando `docker run` según el de tu app.
- **Verifica los logs y errores** usando `docker logs <nombre-contenedor>` si algo no funciona.

---

**¡Con esto dockerizas, construyes y ejecutas tu propio proyecto `mi-proyecto-app` de forma profesional y eficiente!**
