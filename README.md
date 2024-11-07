# Flask and Redis Kubernetes Deployment

This project demonstrates a simple Flask application with Redis as a backend, deployed on Kubernetes using a StatefulSet for Redis and a Deployment for the Flask app. The Flask application connects to Redis for data storage.

## Architecture Overview

The application consists of the following components:
1. **Flask App**: A Python web application that interacts with Redis.
2. **Redis**: A key-value store used by the Flask app for data storage.
3. **Kubernetes Deployment**:
   - **Flask**: Deployed using a `Deployment` resource.
   - **Redis**: Deployed using a `StatefulSet` resource with persistent storage.

## Prerequisites

- A Kubernetes cluster (e.g., Minikube, AWS EKS, GKE, or any local setup).
- `kubectl` configured to access the Kubernetes cluster.
- Helm (optional) if you're using charts for any of the dependencies.
- A container registry or the ability to pull Docker images from public repositories.

## Project Structure

```
.
├── flask-deployment.yaml       # Flask app deployment configuration
├── flask-service.yaml          # Service to expose Flask app
├── redis-pv.yaml               # PersistentVolume for Redis storage
├── redis-pvc.yaml              # PersistentVolumeClaim for Redis storage
├── redis-service.yaml          # Service to expose Redis
└── redis-statefulset.yaml      # StatefulSet for Redis with persistent storage
```

## Getting Started

### 1. Clone the Repository

Clone the repository to your local machine:

```bash
git clone https://github.com/yourusername/flask-redis-k8s.git
cd flask-redis-k8s
```

### 2. Apply Kubernetes Resources

Use the following commands to apply the YAML configurations to your Kubernetes cluster:

```bash
kubectl apply -f redis-pv.yaml
kubectl apply -f redis-pvc.yaml
kubectl apply -f redis-service.yaml
kubectl apply -f redis-statefulset.yaml
kubectl apply -f flask-service.yaml
kubectl apply -f flask-deployment.yaml
```

### 3. Check Resources in the Cluster

Verify that all resources have been created successfully:

```bash
kubectl get all -n web-db-example
```

### 4. Access the Application

If you're using a LoadBalancer service for the Flask app, it will expose an external IP. You can get the external IP using:

```bash
kubectl get svc flask-service -n web-db-example
```

For a local setup, you can use `kubectl port-forward` to expose the Flask app to your localhost:

```bash
kubectl port-forward svc/flask-service 8080:80 -n web-db-example
```

Now, open your browser and visit `http://localhost:8080` to access the Flask app.

### 5. Clean Up

To delete all the resources created, run the following command:

```bash
kubectl delete -f ./
```

## Notes

- **Redis Storage**: The Redis container uses a `PersistentVolume` and `PersistentVolumeClaim` to retain data across pod restarts.
- **Flask App Configuration**: The Flask app is configured to connect to Redis using environment variables `REDIS_HOST` and `REDIS_PORT`.
- **LoadBalancer**: The Flask service is set to `LoadBalancer`. If you don't have a cloud provider with a load balancer, you can change it to `ClusterIP` or use port-forwarding for local setups.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

### How to Customize:

- **GitHub Username**: Replace `yourusername` in the clone URL with your actual GitHub username.
- **License**: Add a `LICENSE` file to the repository if you choose to license the project.
