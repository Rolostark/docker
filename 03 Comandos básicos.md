# 3. docker run, docker ps, docker images, docker pull, docker rm

## ¿Qué aprenderás?
- Comandos básicos para manipular contenedores e imágenes.

---

### Paso 1: docker pull

Descargar una imagen desde Docker Hub:
```bash
docker pull hello-world
```

---

### Paso 2: docker images

Listar imágenes descargadas:
```bash
docker images
```

---

### Paso 3: docker run

Crear y ejecutar un contenedor:
```bash
docker run hello-world
```
Ejecutar en segundo plano y asignar nombre:
```bash
docker run -d --name mi_nginx -p 8080:80 nginx
```

---

### Paso 4: docker ps

Listar contenedores en ejecución:
```bash
docker ps
```
Listar todos (incluidos detenidos):
```bash
docker ps -a
```

---

### Paso 5: docker rm

Eliminar contenedor detenido:
```bash
docker rm mi_nginx
```
Eliminar varios contenedores:
```bash
docker rm cont1 cont2 cont3
```