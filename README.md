# 🐶 Tienda de Alimentos para Perritos

> Plataforma de **e-commerce basada en microservicios**, desplegada sobre **AWS EKS**, con integración de **CI/CD**, escalabilidad automática y monitoreo de infraestructura.

---

# 📖 Descripción del Proyecto

Este proyecto consiste en una plataforma de comercio electrónico para la venta de alimentos para mascotas, desarrollada bajo una arquitectura de microservicios y desplegada en **Amazon Elastic Kubernetes Service (EKS)**.

La solución automatiza completamente el ciclo de vida de despliegue de la aplicación mediante un pipeline de integración y entrega continua (CI/CD), permitiendo realizar actualizaciones rápidas, seguras y sin intervención manual.

Entre sus principales características se encuentran:

* Arquitectura basada en microservicios.
* Contenedores Docker orquestados con Kubernetes.
* Despliegue automático mediante CI/CD.
* Escalado automático según la demanda.
* Alta disponibilidad y tolerancia a fallos.
* Gestión segura de credenciales.

---

# 🏗️ Arquitectura de Infraestructura

La infraestructura se encuentra desplegada sobre servicios administrados de AWS.

## ☁️ Amazon EKS

Se utiliza un clúster llamado **`devopseks`**, encargado de orquestar los contenedores Kubernetes bajo el namespace **`tienda`**, proporcionando:

* Alta disponibilidad.
* Recuperación automática de pods.
* Balanceo interno de carga.
* Escalabilidad horizontal.

---

## 📦 Amazon ECR

Las imágenes Docker son almacenadas en repositorios privados de Amazon Elastic Container Registry.

Repositorios utilizados:

* `tienda-frontend`
* `tienda-backend`
* `tienda-db`

Esto permite mantener un control de versiones y realizar despliegues consistentes.

---

## 🌐 Networking

La aplicación es expuesta mediante un **Application Load Balancer (ALB)** de AWS, encargado de distribuir el tráfico hacia los pods del Frontend.

Beneficios:

* Acceso público a la aplicación.
* Balanceo automático de solicitudes.
* Alta disponibilidad.

---

# ⚙️ Componentes del Proyecto

## Namespace

Se utiliza un namespace llamado **`tienda`** para aislar todos los recursos del proyecto.

---

## Kubernetes Secrets

Las credenciales sensibles son administradas mediante **Secrets**, evitando almacenar información confidencial en texto plano.

Archivo utilizado:

```text
mysql-secret.yaml
```

---

## Base de Datos

La base de datos MySQL se despliega mediante Kubernetes.

Características:

* Servicio tipo **ClusterIP**
* Comunicación únicamente interna
* No expuesta a Internet

---

## Backend

Tecnologías:

* Node.js
* Puerto **3001**

Funciones:

* Gestión de productos
* Comunicación con la base de datos
* Exposición de la API REST

---

## Frontend

Tecnologías:

* Nginx
* Puerto **80**

Funciones:

* Interfaz web para los usuarios
* Consumo de la API del Backend

---

## Horizontal Pod Autoscaler (HPA)

El proyecto implementa **Horizontal Pod Autoscaler** para aumentar o disminuir automáticamente la cantidad de pods según el consumo de CPU.

El HPA utiliza las métricas proporcionadas por **Metrics Server**.

---

# 🚀 Pipeline CI/CD

El flujo de integración y despliegue continuo automatiza completamente el proceso de publicación de nuevas versiones.

Flujo de trabajo:

```text
Developer
      │
      ▼
 Git Push / Commit
      │
      ▼
 Pipeline CI/CD
      │
      ├── Compilación
      ├── Build Docker
      ├── Push a Amazon ECR
      └── Deploy en Amazon EKS
                 │
                 ▼
          Aplicación Actualizada
```

Beneficios:

* Despliegues automáticos.
* Menor tiempo de entrega.
* Reducción de errores humanos.
* Integración continua.

---

# 📊 Monitoreo y Validación

## Metrics Server

El proyecto utiliza **Metrics Server** para recopilar métricas de consumo de CPU y memoria de los pods.

Estas métricas permiten que el HPA tome decisiones de escalado de manera automática.

---

## Horizontal Pod Autoscaler

Durante las pruebas de carga se verificó que:

* El consumo de CPU aumenta.
* El HPA detecta la carga.
* Kubernetes crea nuevas réplicas automáticamente.
* El sistema mantiene la disponibilidad del servicio.

---

## Logs

La comunicación entre los distintos microservicios puede verificarse mediante comandos de Kubernetes como:

```bash
kubectl logs
kubectl get pods
kubectl describe pod
kubectl get hpa
```

Estos comandos permiten auditar el funcionamiento entre:

* Frontend
* Backend
* Base de Datos

---

# 📸 Evidencias Recomendadas

Durante la presentación es recomendable mostrar capturas de:

* Clúster de Amazon EKS.
* Repositorios en Amazon ECR.
* Pods en ejecución.
* Services.
* Deployment.
* Horizontal Pod Autoscaler.
* Metrics Server.
* Balanceador de carga (ALB).
* Sitio web funcionando.
* Pipeline CI/CD exitoso.

---

# 🎤 Guía para la Defensa

## 🔹 Automatización (IE4)

> El flujo de despliegue es completamente automatizado. Cada commit ejecuta un pipeline que compila la aplicación, genera las imágenes Docker, las publica en Amazon ECR y actualiza automáticamente el clúster de Amazon EKS, eliminando la necesidad de intervención manual y reduciendo significativamente los tiempos de despliegue.

---

## 🔹 Seguridad (IE5)

> La seguridad de las credenciales se implementó mediante Kubernetes Secrets. Las contraseñas de la base de datos no se almacenan en texto plano dentro de los manifiestos, sino que son inyectadas de forma segura durante la ejecución de los contenedores.

---

## 🔹 Escalabilidad y Métricas (IE3 / IE6)

> El proyecto incorpora Metrics Server junto con Horizontal Pod Autoscaler. Durante las pruebas de carga se comprobó que, al aumentar el consumo de CPU, Kubernetes incrementa automáticamente el número de réplicas para mantener la disponibilidad del sistema, lo que puede observarse mediante el comando `kubectl get hpa --watch`.

---

## 🔹 Validación Funcional (IE7)

> La comunicación entre los microservicios se realiza mediante el DNS interno de Kubernetes. El Frontend consume la API del Backend, el Backend accede a la base de datos MySQL y la aplicación es publicada mediante un Application Load Balancer de AWS, validando el correcto funcionamiento del sistema de extremo a extremo.

---

# 🛠️ Tecnologías Utilizadas

* AWS EKS
* Kubernetes
* Docker
* Amazon ECR
* MySQL
* Node.js
* Nginx
* Metrics Server
* Horizontal Pod Autoscaler (HPA)
* CI/CD
* Git
* GitHub

---

# 📌 Objetivos Alcanzados

* Arquitectura basada en microservicios.
* Contenedores Docker desplegados en Kubernetes.
* Registro de imágenes en Amazon ECR.
* Orquestación mediante Amazon EKS.
* Gestión segura de credenciales con Secrets.
* Escalado automático mediante HPA.
* Monitoreo utilizando Metrics Server.
* Balanceo de carga mediante AWS ALB.
* Pipeline CI/CD completamente automatizado.
* Plataforma desplegada y funcional.
