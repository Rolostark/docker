# 12. Slim images (Alpine, Distroless), BuildKit

## ¿Qué aprenderás?
- Utilizar imágenes ligeras.
- Aprovechar BuildKit para builds eficientes.

---

### Paso 1: Imágenes ligeras

Usar Alpine:
```Dockerfile
FROM node:18-alpine
```

Usar Distroless (requiere build multistage):
```Dockerfile
# Build
FROM golang:1.20 AS build
WORKDIR /app
COPY . .
RUN go build -o miapp

# Final
FROM gcr.io/distroless/base
COPY --from=build /app/miapp /
CMD ["/miapp"]
```

---

### Paso 2: Activar y usar BuildKit

Activar temporalmente:
```bash
DOCKER_BUILDKIT=1 docker build -t miapp .
```

Activar permanente (Linux):
```bash
echo '{ "features": { "buildkit": true } }' | sudo tee /etc/docker/daemon.json
sudo systemctl restart docker
```