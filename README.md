# Student Task Tracker — CI/CD Practical

## 1. Project Overview

Student Task Tracker is a simple Flask web application developed to demonstrate Continuous Integration and Continuous Deployment (CI/CD) using GitHub, Jenkins, Docker, Docker Hub, and Kubernetes.

## 2. Features

- View and add study tasks
- Mark tasks as complete or pending
- Health-check endpoint at `/health`
- Version endpoint at `/version`
- Containerized deployment using Docker
- Kubernetes Deployment and NodePort Service

Tasks are stored in memory and reset when the application restarts. This keeps the academic project simple and database-free.

## 3. Technologies Used

- Python and Flask
- Git and GitHub
- Jenkins
- Docker and Docker Hub
- Kubernetes
- YAML

## 4. GitHub Repository

Repository: https://github.com/Mansigunjal/student-task-tracker-cicd

## 5. Docker Hub Image

Docker Hub repository: https://hub.docker.com/r/mansig1/student-task-tracker

Image name: `mansig1/student-task-tracker:latest`

## 6. Run the Application Locally

Install the dependencies:

```bash
pip install -r requirements.txt
```

Start the application:

```bash
python app.py
```

Open `http://localhost:5000` in your browser.

## 7. Run Tests

```bash
pytest -q
```

## 8. Build and Run with Docker

Build the Docker image:

```bash
docker build -t student-task-tracker:local .
```

Run the container:

```bash
docker run -d -p 5000:5000 --name student-task-tracker student-task-tracker:local
```

Open `http://localhost:5000`.

## 9. Kubernetes Deployment

Apply the Deployment configuration:

```bash
kubectl apply -f deployment.yaml
```

Apply the Service configuration:

```bash
kubectl apply -f service.yaml
```

Verify the Deployment, pods, and Services:

```bash
kubectl get deployments
kubectl get pods
kubectl get services
```

Forward the Service port to access the application locally:

```bash
kubectl port-forward service/student-task-tracker 8081:5000
```

Open `http://localhost:8081` while port forwarding is running.

The application was verified using Docker Desktop Kubernetes. The assignment's Minikube requirement remains to be completed separately.

## 10. Jenkins Pipeline

The `Jenkinsfile` defines the following stages:

1. Checkout source code from GitHub.
2. Install Python dependencies and run tests.
3. Build the Docker image.
4. Push the versioned image and `latest` tag to Docker Hub.
5. Apply Kubernetes configurations and verify deployment status.

### Jenkins configuration requirements

- Jenkins must be running on a Linux agent with Python, Docker, and the required tools installed.
- Configure a Jenkins credential with ID `dockerhub-creds` using a Docker Hub username and access token.
- Configure access to the Kubernetes cluster that Jenkins will deploy to.
- Create a Jenkins Pipeline job connected to this repository and the `Jenkinsfile`.

**Note:** The Jenkins pipeline has not yet been verified end-to-end. Jenkins is responding locally on the EC2 instance, but its web interface has been unreachable from the laptop. A Kubernetes cluster must also be accessible to the Jenkins agent for the deployment stage to succeed.

## 11. Demonstration and Evidence

Capture screenshots showing:

- The Student Task Tracker running in a browser
- Docker Hub repository and image tag
- Kubernetes Deployment status
- Kubernetes pod in the `Running` state
- Kubernetes Service output
- Jenkins pipeline execution, once successfully configured

For the source-change demonstration, update the response from `/version`, commit and push the change, and verify that the pipeline builds and deploys the updated image.

## 12. Conclusion

This project demonstrates a Flask application packaged with Docker, stored in Docker Hub, and deployed to Kubernetes. GitHub stores the source code and CI/CD configuration. Jenkins is configured in the repository to automate testing, image building, publishing, and deployment, subject to Jenkins connectivity and Kubernetes access being configured and verified.
