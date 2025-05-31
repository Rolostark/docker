# 1. Contenedores vs VMs, Imágenes, Contenedores, Docker Engine, Arquitectura de Docker

## ¿Qué aprenderás?
- Diferencias entre contenedores y máquinas virtuales.
- Qué son imágenes y contenedores.
- Componentes de la arquitectura Docker.

---

### Paso 1: Contenedores vs VMs

| Contenedor                | Máquina Virtual               |
|---------------------------|------------------------------|
| Ligero, rápido de iniciar | Más pesado, lento de iniciar |
| Comparte kernel del host  | Kernel propio                |
| Aislamiento a nivel OS    | Aislamiento completo         |

---

### Paso 2: ¿Qué es una imagen y un contenedor?

- **Imagen:** Plantilla inmutable, solo lectura, para crear contenedores.
- **Contenedor:** Instancia en ejecución de una imagen.

```bash
# Descargar y ejecutar una imagen de nginx
docker run --name miweb -d -p 8080:80 nginx
```

---

### Paso 3: Docker Engine

- Motor de Docker que administra imágenes, contenedores, redes y volúmenes.

---

### Paso 4: Arquitectura de Docker

1. **Cliente Docker (CLI):** Interfaz de usuario.
2. **Docker Daemon:** Maneja objetos de Docker.
3. **REST API:** Comunicación entre cliente y daemon.
4. **Registros:** Almacenan imágenes (ej. Docker Hub).

```
[Usuario] -> [CLI] -> [Docker Daemon] <-> [Docker Hub]
```