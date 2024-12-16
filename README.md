Portfolio Website Deployment on Kubernetes
🚀 Project Overview
This project demonstrates the deployment of a portfolio website using modern DevOps practices. It leverages Docker, AWS EKS, and Kubernetes to containerize, deploy, and manage a scalable and highly available web application.

🛠️ Technologies Used
Docker: Containerization of the portfolio application.
Kubernetes (EKS): Orchestration platform to manage containers.
AWS: Elastic Kubernetes Service (EKS) and Load Balancer for deployment.
Nginx: Web server to host the portfolio.
GitHub: Repository management for source code and CI/CD.
Linux (Ubuntu): Development and deployment environment.
VS Code: IDE for development.
📂 Project Structure
plaintext
Copy code
portfolio/
├── deployment.yaml   # Kubernetes deployment configuration
├── service.yaml      # Kubernetes service configuration
├── Dockerfile        # Docker configuration for containerizing the app
├── index.html        # Portfolio HTML file
├── styles.css        # Styling for the portfolio website
📝 Key Steps
1. Website Development
Created custom HTML (index.html) and CSS (styles.css) for the portfolio in VS Code.
Designed a simple layout showcasing a DevOps engineer’s skills and achievements.
2. Docker Containerization
Created a Dockerfile to containerize the application:
dockerfile
Copy code
FROM nginx:latest
COPY . /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
Built and pushed the Docker image to DockerHub:
bash
Copy code
docker build -t aidanadevops2023/my-website:latest .
docker push aidanadevops2023/my-website:latest
3. Kubernetes Deployment
Created a deployment.yaml file for Kubernetes to manage the pods:
yaml
Copy code
apiVersion: apps/v1
kind: Deployment
metadata:
  name: portfolio
  labels:
    app: my-website
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-website
  template:
    metadata:
      labels:
        app: my-website
    spec:
      containers:
        - name: portfolio
          image: aidanadevops2023/my-website:latest
          ports:
            - containerPort: 80
Applied the deployment:
bash
Copy code
kubectl apply -f deployment.yaml
4. Service Configuration
Created a service.yaml to expose the deployment using a LoadBalancer:
yaml
Copy code
apiVersion: v1
kind: Service
metadata:
  name: my-website-service
spec:
  type: LoadBalancer
  selector:
    app: my-website
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
Applied the service:
bash
Copy code
kubectl apply -f service.yaml
5. Deployment on AWS EKS
Set up an EKS cluster using eksctl:
bash
Copy code
eksctl create cluster --name my-eks-cluster --region us-east-1 --nodes 2 --node-type t3.micro
Configured kubectl for the cluster:
bash
Copy code
aws eks update-kubeconfig --region us-east-1 --name my-eks-cluster
6. Testing and Verification
Verified the pods and service:
bash
Copy code
kubectl get pods
kubectl describe service my-website-service
Accessed the portfolio using the LoadBalancer's external IP:
arduino
Copy code
http://<external-ip>
🎯 Key Features
Scalable Deployment: Kubernetes ensures scalability with replicas.
Highly Available: Load Balancer distributes traffic across pods.
Containerized Application: Portable and consistent environment using Docker.
🛡️ Future Enhancements
Implement CI/CD pipelines using GitHub Actions.
Use Terraform for infrastructure as code (IaC).
Integrate Prometheus and Grafana for monitoring.
Automate deployments with Ansible.
📌 Usage
To replicate this setup:

Clone the repository:
bash
Copy code
git clone <repository-url>
Build and push the Docker image:
bash
Copy code
docker build -t <your-dockerhub-repo>/my-website:latest .
docker push <your-dockerhub-repo>/my-website:latest
Apply Kubernetes manifests:
bash
Copy code
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
Access the app via the LoadBalancer external IP.

## Website
Visit the live website: https://aidana-devops.github.io/portfolio-website/

## Technologies Used
- Docker
- Kubernetes
- AWS EKS
- Nginx



