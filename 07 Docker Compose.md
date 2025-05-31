# 7. Archivos docker-compose.yml, Servicios, redes, volúmenes

## ¿Qué aprenderás?
- Definir multi-contenedores con docker-compose.
- Uso de servicios, redes y volúmenes.

---

### Paso 1: Ejemplo básico de docker-compose.yml

```yaml
version: "3.8"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
    volumes:
      - html:/usr/share/nginx/html
  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: ejemplo
    volumes:
      - datosdb:/var/lib/mysql
volumes:
  html:
  datosdb:
```

---

### Paso 2: Comandos básicos

Arrancar:
```bash
docker-compose up -d
```
Parar:
```bash
docker-compose down
```