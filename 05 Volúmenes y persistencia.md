# 5. Bind mounts, Volúmenes nombrados y docker volume

## ¿Qué aprenderás?
- Cómo lograr persistencia de datos en Docker.
- Diferencias clave entre bind mounts y volúmenes.
- Cómo crear, usar y administrar volúmenes con `docker volume`.

---

### Paso 1: Bind mounts

Un **bind mount** conecta una carpeta del sistema anfitrión (host) con una ruta dentro del contenedor. Así, los cambios en el host se reflejan al instante en el contenedor y viceversa.

**Ejemplo:** Montar la carpeta actual del host en `/app` del contenedor:
```bash
docker run -v $(pwd):/app node:18
```
- Los archivos que edites en tu máquina local se verán directamente dentro del contenedor.
- Útil para desarrollo y pruebas.

---

### Paso 2: Volúmenes nombrados

Un **volumen nombrado** es gestionado por Docker. Su ruta física está oculta (por defecto en `/var/lib/docker/volumes/`).

**Crear y usar un volumen:**
```bash
docker volume create datos
docker run -v datos:/data busybox
```
- Docker se encarga de la ubicación y el ciclo de vida del volumen.
- Los datos persisten aunque el contenedor se elimine.
- Ideal para entornos de producción y compartir datos entre contenedores.

---

### Paso 3: Gestionar volúmenes

#### Listar volúmenes disponibles:
```bash
docker volume ls
```

#### Inspeccionar un volumen:
```bash
docker volume inspect datos
```

#### Eliminar un volumen:
```bash
docker volume rm datos
```

> **Nota:** No puedes eliminar un volumen que está siendo usado por un contenedor en ejecución.

---

### Resumen

- **Bind mounts:** Compartes carpetas/archivos del host con el contenedor; útil para desarrollo.
- **Volúmenes nombrados:** Docker los administra; ideales para producción y compartir datos.
- **Comandos útiles:** `docker volume create`, `docker volume ls`, `docker volume inspect`, `docker volume rm`.
