# 4. Sintaxis de Dockerfile y Buenas Prácticas (Multistage)

## ¿Qué aprenderás?
- Estructura de un Dockerfile.
- Buenas prácticas: imágenes multistage para optimizar tamaño y seguridad.

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

**Visual del flujo:**

```
Tu código fuente
      |
      v
+--------------------+
|    Dockerfile      |
+--------------------+
      |
      v
+--------------------+
|    Imagen Docker   |
+--------------------+
      |
      v
+--------------------+
| Contenedor listo   |
+--------------------+
```

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

**¿Cómo funciona?**

1. **Etapa de Build:**  
   - Instala dependencias y genera archivos en `/app/dist`.
   - Contiene herramientas de desarrollo y todo el código fuente.

2. **Etapa Final:**  
   - Usa una imagen base más ligera (`node:18-slim`).
   - Solo copia los archivos necesarios para ejecutar la app (`/app/dist`).
   - No incluye dependencias de desarrollo, código fuente ni herramientas innecesarias.

**Visual del flujo multistage:**

```
+---------------------+
|   Etapa 1: build    |
|  node:18            |
|  + npm install      |
|  + npm run build    |
+----------+----------+
           |
           |  (Solo /app/dist se copia)
           v
+---------------------+
|   Etapa 2: final    |
|  node:18-slim       |
|  + /app/dist        |
|  + node dist/index  |
+---------------------+
```

---

## Consejos adicionales de buenas prácticas

- **Usa `.dockerignore`** para evitar copiar archivos innecesarios.
- **Define variables de entorno** con `ENV` si es necesario.
- **No uses root**: especifica un usuario no root para mayor seguridad (`USER`).
- **Agrupa comandos RUN** para reducir capas.
- **Prefiere imágenes oficiales y ligeras** (`-slim`, `-alpine`).

---

**¡Con esto podrás escribir Dockerfiles eficientes y seguros para tus proyectos!**
