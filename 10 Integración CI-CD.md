# 10. Docker en GitHub Actions/GitLab CI, Buildx para multi-arch

## ¿Qué aprenderás?
- Usar Docker en pipelines CI/CD.
- Buildx para imágenes multi-arquitectura.

---

### Paso 1: Docker en GitHub Actions

Ejemplo `.github/workflows/docker.yml`:
```yaml
name: Build and Push Docker Image
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
      - name: Login to DockerHub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
      - name: Build and Push
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: usuario/imagen:latest
```

---

### Paso 2: Buildx para multi-arch

```bash
docker buildx create --use
docker buildx build --platform linux/amd64,linux/arm64 -t usuario/imagen:multiarch --push .
```