# 5. Bind mounts, Volúmenes nombrados, docker volume

## ¿Qué aprenderás?
- Persistencia de datos con Docker.
- Diferencias entre bind mounts y volúmenes.
- Uso de `docker volume`.

---

### Paso 1: Bind mounts

Montar una carpeta del host en el contenedor:

```bash
docker run -v $(pwd):/app node:18
```
- Cambios en el host se reflejan en el contenedor.

---

### Paso 2: Volúmenes nombrados

Crear y usar un volumen:

```bash
docker volume create datos
docker run -v datos:/data busybox
```
- Docker administra la ubicación.

---

### Paso 3: Gestionar volúmenes

Listar:
```bash
docker volume ls
```
Inspeccionar:
```bash
docker volume inspect datos
```
Eliminar:
```bash
docker volume rm datos
```