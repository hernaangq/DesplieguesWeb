# WebDeployments
### Hernán García Quijano · Eric Ordás Martín · Luis Núñez Casal

This is our **Creative Project 2** from the 2023–2024 **CDPS** course (Design and Deployment of Distributed Systems) at **ETSIT‑UPM**.

---

## 🌐 Full Application Deployment Scenario

We developed a complete scenario to deploy a **reliable and scalable application**, integrating key topics from the course. The project consolidates knowledge in **cloud-based deployments** and **microservices architectures** using **Docker** and **Kubernetes**.

The deployment is organized into five major blocks:

- Deployment of a monolithic application on a Google Cloud virtual machine.
- Deployment of a monolithic application using Docker.
- Segmentation of a monolithic app into microservices with Docker Compose.
- Deployment of a microservices-based app using Kubernetes.
- Deployment of the same system with **Helm Charts**.

---

## 🧱 1. Monolithic App on Google Cloud VM

**Steps:**

1. Create a new VM instance in Google Cloud.
2. Configure a firewall rule to allow all traffic.

```bash
cd bloque1
python3 bloque1.py arrancar
````

The app will run at the external IP on port `9080`.

Use this to specify a custom port:

```bash
python3 bloque1.py arrancarPuerto [port]
```

To destroy the setup:

```bash
python3 bloque1.py liberar
```

---

## 🐳 2. Monolithic App with Docker

You can reuse the VM from Block 1.

```bash
cd bloque2
python3 bloque2.py crear
python3 bloque2.py arrancar
```

To tear it down:

```bash
python3 bloque2.py liberar
```

---

## 🔧 3. Microservices with Docker Compose

You can also reuse the VM from previous blocks.

```bash
cd bloque3
python3 bloque3.py
```

This will launch the microservices-based version of the application at the external IP on port `9080`.

---

## ☸️ 4. Microservices with Kubernetes (GKE)

1. Create a **Kubernetes Engine** cluster on Google Cloud.

2. Apply all necessary manifests:

```bash
cd bloque4
kubectl apply -f productpage.yaml
kubectl apply -f details.yaml
kubectl apply -f ratings.yaml
kubectl apply -f reviews-svc.yaml
kubectl apply -f review-<version>-<type>.yaml
```

To check services and deployments:

```bash
kubectl get all
```

To delete the environment:

```bash
kubectl delete --all deployments && kubectl delete --all pods && kubectl delete --all services
```

---

## ⚙️ \[Optional] Deployment with Helm Charts

Helm is already available in GKE.

Steps:

```bash
helm create prueba
cd prueba
```

* Copy all your YAML manifests into the `templates` directory.
* Edit `values.yaml` to set the image repo and target port.

To deploy:

```bash
helm install prueba .
```

To get the external IP:

```bash
kubectl get services
```

View in browser:

```text
http://<external-ip>:9080/productpage
```

To delete everything:

```bash
kubectl delete --all deployments && kubectl delete --all pods && kubectl delete --all services
```

---

## 📬 Contact

* **Hernán García Quijano**: [hernan.garcia.quijano@alumnos.upm.es](mailto:hernan.garcia.quijano@alumnos.upm.es)
* **Eric Ordás Martín**: [e.ordar@alumnos.upm.es](mailto:e.ordar@alumnos.upm.es)
* **Luis Núñez Casal**: [luisignacio.nunez@alumnos.upm.es](mailto:luisignacio.nunez@alumnos.upm.es)



