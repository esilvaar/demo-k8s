# 🚀 Demo Kubernetes App

## 📌 Descripción

Este proyecto consiste en una aplicación web simple desarrollada con Node.js y Express, la cual fue contenerizada con Docker y desplegada en Kubernetes usando Minikube.

La aplicación responde con el mensaje:

Hola desde Kubernetes 🚀

---

## 🎯 Objetivo

Demostrar el flujo real de despliegue de una aplicación moderna:

Desarrollo → Contenedor → Orquestación → Acceso

---

## 🧱 Arquitectura

Aplicación Node.js  
↓  
Imagen Docker  
↓  
Kubernetes (Minikube)  
↓  
Deployment (Pods)  
↓  
Service (NodePort)  
↓  
Acceso vía navegador  

---

## ⚙️ Tecnologías utilizadas

- Node.js
- Express
- Docker
- Kubernetes
- Minikube
- kubectl

---

## 📁 Estructura del proyecto

demo-k8s/
│
├── index.js
├── package.json
├── Dockerfile
└── k8s/
    ├── deployment.yaml
    └── service.yaml

---

## 🐳 Docker

### ¿Qué hace el Dockerfile?

El Dockerfile define cómo construir la imagen de la aplicación:

- Usa una imagen base de Node.js
- Copia archivos del proyecto
- Instala dependencias
- Expone el puerto 3000
- Ejecuta la aplicación

### Construir la imagen

docker build -t demo-app:1.0 .

### Ejecutar el contenedor

docker run -p 3000:3000 demo-app:1.0

---

## ☸️ Kubernetes

### Deployment

El archivo deployment.yaml:

- Crea múltiples réplicas de la aplicación (Pods)
- Ejecuta el contenedor demo-app
- Mantiene el estado deseado

Aplicar:

kubectl apply -f k8s/deployment.yaml

Ver Pods:

kubectl get pods

---

### Service

El archivo service.yaml:

- Expone la aplicación hacia el exterior
- Usa NodePort para acceso local
- Redirige tráfico del puerto 80 al 3000

Aplicar:

kubectl apply -f k8s/service.yaml

Acceder:

minikube service demo-service

---

## 📈 Escalamiento

Para aumentar la cantidad de Pods:

kubectl scale deployment demo-app --replicas=4

Kubernetes crea automáticamente nuevos Pods y distribuye el tráfico.

---

## ♻️ Resiliencia

Si un Pod falla:

kubectl delete pod <nombre-del-pod>

Kubernetes lo recrea automáticamente para mantener el estado.

---

## ☁️ Preparación para la nube

Este proyecto puede desplegarse en la nube usando servicios como:

- AWS EKS
- Azure AKS
- Google GKE

### Cambios necesarios:

- Subir la imagen a un registry (Docker Hub, ECR, etc.)
- Cambiar el Service a:

type: LoadBalancer

Esto permitirá acceso público mediante IP o DNS.

---

## 🧠 ¿Qué hace Kubernetes?

Kubernetes se encarga de:

- Ejecutar contenedores
- Escalar la aplicación
- Recuperar servicios en caso de fallos
- Balancear el tráfico
- Gestionar el estado deseado

---

## ✅ Conclusión

Este laboratorio demuestra el flujo completo de despliegue moderno:

- Desarrollo local
- Contenerización con Docker
- Orquestación con Kubernetes
- Escalabilidad y alta disponibilidad

---

## 👨‍💻 Autor

Eduar