# 9. Capabilities, User namespaces, Scanning (Trivy, Clair)

## ¿Qué aprenderás?
- Seguridad con capabilities y user namespaces.
- Escaneo de imágenes.

---

### Paso 1: Capabilities

Limitar capacidades del contenedor:
```bash
docker run --cap-drop=ALL --cap-add=NET_BIND_SERVICE nginx
```

---

### Paso 2: User namespaces

Ejecutar contenedor con usuario no root:
```bash
docker run -u 1000:1000 nginx
```

---

### Paso 3: Scanning de imágenes

Escanear con Trivy:
```bash
docker pull alpine
trivy image alpine
```

Escanear con Clair (requiere configuración avanzada):
- Ver [Clair documentation](https://quay.github.io/clair/)

---