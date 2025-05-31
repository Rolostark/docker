# 2. Docker Desktop (Windows/Mac), Docker Engine (Linux)

## ¿Qué aprenderás?
- Diferencias y uso de Docker Desktop y Docker Engine.
- Instalación básica.

---

### Paso 1: Docker Desktop (Windows/Mac)

- Instalador gráfico, incluye Docker Engine, Compose y herramientas extra.
- Requiere virtualización (WSL2 en Windows).

**Instalación:**
1. Descargar desde [docker.com](https://www.docker.com/products/docker-desktop/).
2. Instalar y aceptar términos.
3. Verificar con:
   ```bash
   docker --version
   ```

---

### Paso 2: Docker Engine (Linux)

- Motor principal, ejecutado como servicio.

**Instalación en Ubuntu:**
```bash
sudo apt-get update
sudo apt-get install \
    ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
Verificar:
```bash
docker --version
```