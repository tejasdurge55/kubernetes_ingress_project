# 🚀 Ingress Web App Deployment on Kubernetes

This project demonstrates how to deploy an Ingress web app on Kubernetes using YAML configuration files.

## Prerequisites
- Kubernetes cluster up and running.
- `kubectl` command-line tool installed and configured.

#### 🛠 Skills Required:
- Kubernetes Basics
- Docker

## Deploying the Ingress Web App

### Step 1: Deploy the Demo Applications
You can deploy the applications using the following Kubernetes deployment file deployment.yaml:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo1
spec:
  replicas: 2
  selector:
    matchLabels:
      app: demo1
  template:
    metadata:
      labels:
        app: demo1
    spec:
      containers:
      - name: demo1
        image: tejasdurge55/dice_app
        ports:
        - containerPort: 80

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo2
spec:
  replicas: 3
  selector:
    matchLabels:
      app: demo2
  template:
    metadata:
      labels:
        app: demo2
    spec:
      containers:
      - name: demo2
        image: tejasdurge55/automated_apache_server
        ports:
        - containerPort: 80
```

### Step 2: Create Services for the Deployments
Create Kubernetes services for the deployed applications:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: tea-svc
# ... (service configuration)
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: coffee-svc
# ... (service configuration)
```

### Step 3: Configure Ingress
Configure the Ingress resource to route traffic to the deployed services based on specific paths:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: service-a
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$1
spec:
  ingressClassName: nginx
  rules:
  - host: public.my-services.com
    http:
      paths:
      - path: /(.*)
        pathType: Prefix
        backend:
          service:
            name: tea-svc
            port:
              number: 80
      - path: /gift/(.*)
        pathType: Prefix
        backend:
          service:
            name: coffee-svc
            port:
              number: 80
```

## Deploying the Configuration
Apply the configuration files to your Kubernetes cluster using `kubectl apply -f <file>`.

Make sure to replace `<file>` with the actual file name.

## Accessing Your Ingress Web App
Once deployed and configured, you can access your Ingress web app using the specified host and paths.

Example:
- http://public.my-services.com/
- http://public.my-services.com/gift/

# Thank you! 👋

## 🔗 Connect with Me
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/tejas-durge-0a62a128a/)
[![twitter](https://img.shields.io/badge/twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/TejasDurge55)

