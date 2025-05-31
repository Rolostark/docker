# 6. Redes bridge/host/none, Conectar contenedores (docker network)

## ¿Qué aprenderás?
- Tipos de redes en Docker.
- Conexión de contenedores.

---

### Paso 1: Tipos de redes

- **bridge:** Por defecto, para la mayoría de los contenedores.
- **host:** Sin aislamiento de red, comparte la red del host.
- **none:** Sin red.

---

### Paso 2: Crear red y conectar contenedores

Crear una red personalizada:
```bash
docker network create mi_red
```

Ejecutar contenedores en la misma red:
```bash
docker run -d --name web --network mi_red nginx
docker run -it --rm --network mi_red busybox ping web
```

---

### Paso 3: Listar y administrar redes

Listar:
```bash
docker network ls
```
Eliminar:
```bash
docker network rm mi_red
```