# 11. Custom drivers, Extender Docker con plugins

## ¿Qué aprenderás?
- Crear o usar drivers personalizados.
- Extender Docker con plugins.

---

### Paso 1: Custom network driver (ejemplo)

Instalar un driver de red de terceros:
```bash
docker network create -d weave mynet
```
Más info: [Docker network plugins](https://docs.docker.com/network/plugins/)

---

### Paso 2: Plugins de volumen

Instalar y usar un plugin:
```bash
docker plugin install vieux/sshfs
docker volume create -d vieux/sshfs nombre_volumen
```

---

### Paso 3: Listar y administrar plugins

Listar:
```bash
docker plugin ls
```
Activar/desactivar:
```bash
docker plugin enable vieux/sshfs
docker plugin disable vieux/sshfs
```