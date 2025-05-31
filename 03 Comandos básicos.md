# 3. Comandos Básicos de Docker: `run`, `ps`, `images`, `pull`, `rm`

## ¿Qué aprenderás?
- Cómo descargar imágenes, crear y administrar contenedores, y gestionar imágenes y contenedores en Docker.

---

## 1. Descargar una imagen: `docker pull`

**Comando:**
```bash
docker pull hello-world
```
**¿Qué hace?**  
Descarga la imagen `hello-world` desde Docker Hub a tu máquina local.

**Visual:**
```
+------------------------+
|  Docker Hub (Internet) |
+-----------+------------+
            |
            v
+------------------------+
|   Tu computadora       |
|   [hello-world image]  |
+------------------------+
```

---

## 2. Listar imágenes: `docker images`

**Comando:**
```bash
docker images
```
**¿Qué hace?**  
Muestra todas las imágenes que tienes descargadas localmente.

**Visual:**
```
+-------------------------------+
| Imágenes Locales              |
+-------------------------------+
| REPOSITORY   TAG   IMAGE ID   |
| hello-world  latest ...       |
| nginx        latest ...       |
+-------------------------------+
```

---

## 3. Crear y ejecutar un contenedor: `docker run`

**Ejemplo 1: Ejecutar una imagen sencilla**
```bash
docker run hello-world
```
Esto crea y ejecuta un contenedor basado en la imagen `hello-world`.

**Ejemplo 2: Ejecutar en segundo plano y exponer un puerto**
```bash
docker run -d --name mi_nginx -p 8080:80 nginx
```
- `-d`: Ejecuta el contenedor en segundo plano (detached).
- `--name mi_nginx`: Asigna el nombre `mi_nginx` al contenedor.
- `-p 8080:80`: Mapea el puerto 80 del contenedor al 8080 de tu máquina.

**Visual:**
```
+----------------------+
|    Contenedor        |
|  [nginx en ejecución]|
+----------+-----------+
           |
         8080 (tu PC)
```

---

## 4. Ver contenedores: `docker ps`

**Comando para ver contenedores activos:**
```bash
docker ps
```
**Comando para ver todos (incluyendo detenidos):**
```bash
docker ps -a
```

**Visual:**
```
+--------------------------------------+
| Contenedores en ejecución            |
+--------------------------------------+
| CONTAINER ID  IMAGE   STATUS   PORTS |
| a1b2c3d4e5f6  nginx   Up ...  8080->80|
+--------------------------------------+
```

---

## 5. Eliminar contenedores: `docker rm`

**Eliminar un contenedor detenido:**
```bash
docker rm mi_nginx
```
**Eliminar varios contenedores a la vez:**
```bash
docker rm cont1 cont2 cont3
```

**Nota:**  
Solo puedes eliminar contenedores que estén detenidos.

**Visual:**
```
Antes:
[mi_nginx] [cont2] [cont3] ... (detenidos)
    |
docker rm mi_nginx cont2 cont3
    |
Después:
[...Contenedores eliminados...]
```

---

## Resumen visual del flujo típico

```
1. docker pull <imagen>        # Descargar imagen
2. docker images               # Ver imágenes locales
3. docker run <imagen>         # Crear y ejecutar contenedor
4. docker ps / docker ps -a    # Ver contenedores
5. docker rm <contenedor>      # Eliminar contenedores detenidos
```

---

**¡Ahora puedes administrar imágenes y contenedores Docker como un profesional!**
