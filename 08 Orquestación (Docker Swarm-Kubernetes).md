# 8. Swarm: nodos, servicios, stacks, Kubernetes: pods, deployments

## ¿Qué aprenderás?
- Orquestación con Docker Swarm y una visión básica de Kubernetes.

---

### Paso 1: Docker Swarm

Inicializar Swarm:
```bash
docker swarm init
```

Crear un servicio:
```bash
docker service create --name web -p 80:80 nginx
```

Listar nodos y servicios:
```bash
docker node ls
docker service ls
```

Stacks (multi-contenedores):
```bash
docker stack deploy -c docker-compose.yml mystack
```

---

### Paso 2: Kubernetes conceptos básicos

- **Pod:** Unidad mínima, puede contener varios contenedores.
- **Deployment:** Gestiona el ciclo de vida de pods.

Ejemplo de deployment:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: miapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: miapp
  template:
    metadata:
      labels:
        app: miapp
    spec:
      containers:
        - name: web
          image: nginx
          ports:
            - containerPort: 80
```