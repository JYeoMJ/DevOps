# Comprehensive DevOps Cheat Sheet: Docker, Kubernetes, and OpenShift

## Table of Contents
1. [Docker CLI](#docker-cli)
2. [Kubernetes Architecture](#kubernetes-architecture)
3. [Managing Applications with Kubernetes](#managing-applications-with-kubernetes)
4. [OpenShift CLI](#openshift-cli)
5. [Common Workflows](#common-workflows)
6. [Best Practices](#best-practices)
7. [Troubleshooting Tips](#troubleshooting-tips)

## Docker CLI

### Basic Docker Commands
| Command | Description | Example |
|---------|-------------|---------|
| `docker --version` | Displays the version of the Docker CLI. | `docker --version` |
| `docker info` | Display system-wide information | `docker info` |
| `docker login` | Log in to a Docker registry | `docker login my-registry.com` |
| `docker logout` | Log out from a Docker registry | `docker logout my-registry.com` |

### Image Management
| Command | Description | Example |
|---------|-------------|---------|
| `docker build` | Builds an image from a Dockerfile. | `docker build -t myapp:1.0 .` |
| `docker images` | Lists the images. | `docker images` |
| `docker pull` | Pulls an image or a repository from a registry. | `docker pull ubuntu:latest` |
| `docker push` | Pushes an image or a repository to a registry. | `docker push myregistry/myapp:1.0` |
| `docker tag` | Creates a tag TARGET_IMAGE that refers to SOURCE_IMAGE | `docker tag myapp:latest myregistry/myapp:v1` |
| `docker rmi` | Removes one or more images | `docker rmi myapp:oldversion` |

### Container Operations
| Command | Description | Example |
|---------|-------------|---------|
| `docker run` | Runs a command in a new container. | `docker run -d -p 80:80 nginx` |
| `docker ps` | Lists running containers. | `docker ps` |
| `docker ps -a` | Lists all containers (running and stopped). | `docker ps -a` |
| `docker stop` | Stops one or more running containers. | `docker stop mycontainer` |
| `docker start` | Starts one or more stopped containers | `docker start mycontainer` |
| `docker restart` | Restarts one or more containers | `docker restart mycontainer` |
| `docker rm` | Removes one or more containers | `docker rm myoldcontainer` |
| `docker logs` | Fetch the logs of a container | `docker logs --tail 100 mycontainer` |
| `docker exec` | Run a command in a running container | `docker exec -it mycontainer /bin/bash` |

### Network Management
| Command | Description | Example |
|---------|-------------|---------|
| `docker network create` | Creates a new network | `docker network create mynetwork` |
| `docker network ls` | Lists all networks | `docker network ls` |
| `docker network rm` | Removes one or more networks | `docker network rm myoldnetwork` |

### Volume Management
| Command | Description | Example |
|---------|-------------|---------|
| `docker volume create` | Creates a volume | `docker volume create myvolume` |
| `docker volume ls` | Lists all volumes | `docker volume ls` |
| `docker volume rm` | Removes one or more volumes | `docker volume rm myoldvolume` |

### IBM Cloud Container Registry
| Command | Description | Example |
|---------|-------------|---------|
| `ibmcloud cr login` | Logs your local Docker daemon into IBM Cloud Container Registry. | `ibmcloud cr login` |
| `ibmcloud cr namespace-add` | Creates a namespace in IBM Cloud Container Registry | `ibmcloud cr namespace-add mynamespace` |
| `ibmcloud cr image-list` | Lists images in IBM Cloud Container Registry | `ibmcloud cr image-list` |
| `ibmcloud cr image-rm` | Deletes one or more images from IBM Cloud Container Registry | `ibmcloud cr image-rm us.icr.io/mynamespace/myimage:latest` |

## Kubernetes Architecture

### Cluster Management
| Command | Description | Example |
|---------|-------------|---------|
| `kubectl config view` | Displays merged kubeconfig settings | `kubectl config view` |
| `kubectl config get-clusters` | Displays clusters defined in the kubeconfig | `kubectl config get-clusters` |
| `kubectl config get-contexts` | Displays the current context | `kubectl config get-contexts` |
| `kubectl config use-context` | Sets the current-context in a kubeconfig file | `kubectl config use-context my-cluster` |
| `kubectl cluster-info` | Display cluster information | `kubectl cluster-info` |

### Resource Management
| Command | Description | Example |
|---------|-------------|---------|
| `kubectl apply` | Applies a configuration to a resource | `kubectl apply -f deployment.yaml` |
| `kubectl create` | Creates a resource | `kubectl create deployment nginx --image=nginx` |
| `kubectl delete` | Deletes resources | `kubectl delete pod mypod` |
| `kubectl edit` | Edit a resource on the server | `kubectl edit deployment/myapp` |
| `kubectl get` | List one or many resources | `kubectl get pods` |
| `kubectl describe` | Show detailed information about a resource | `kubectl describe pod mypod` |

### Namespaces and Context
| Command | Description | Example |
|---------|-------------|---------|
| `kubectl create namespace` | Creates a namespace | `kubectl create namespace myspace` |
| `kubectl get namespaces` | Lists all namespaces | `kubectl get namespaces` |
| `kubectl config set-context` | Sets a context entry in kubeconfig | `kubectl config set-context --current --namespace=myspace` |

## Managing Applications with Kubernetes

### Deployment Operations
| Command | Description | Example |
|---------|-------------|---------|
| `kubectl create deployment` | Creates a deployment | `kubectl create deployment myapp --image=myimage` |
| `kubectl scale deployment` | Scales a deployment | `kubectl scale deployment myapp --replicas=3` |
| `kubectl set image deployment` | Updates image of a deployment | `kubectl set image deployment/myapp myapp=myapp:v2` |
| `kubectl rollout status deployment` | Check the rollout status of a deployment | `kubectl rollout status deployment/myapp` |
| `kubectl rollout undo deployment` | Rollback to a previous deployment | `kubectl rollout undo deployment/myapp` |

### Service Operations
| Command | Description | Example |
|---------|-------------|---------|
| `kubectl expose` | Expose a resource as a new Kubernetes service | `kubectl expose deployment myapp --type=LoadBalancer --port=8080` |
| `kubectl get services` | List all services in the namespace | `kubectl get services` |

### ConfigMaps and Secrets
| Command | Description | Example |
|---------|-------------|---------|
| `kubectl create configmap` | Create a configmap from directories, files, or literal values | `kubectl create configmap myconfig --from-file=path/to/dir` |
| `kubectl create secret` | Create a secret using specified subcommand | `kubectl create secret generic mysecret --from-literal=password=mypass` |

### Autoscaling
| Command | Description | Example |
|---------|-------------|---------|
| `kubectl autoscale deployment` | Autoscales a Kubernetes Deployment | `kubectl autoscale deployment myapp --min=2 --max=5 --cpu-percent=80` |
| `kubectl get hpa` | List all horizontal pod autoscalers | `kubectl get hpa` |

## OpenShift CLI

| Command | Description | Example |
|---------|-------------|---------|
| `oc login` | Log in to your OpenShift cluster | `oc login https://api.myopenshift.com` |
| `oc project` | Switch to another project | `oc project myproject` |
| `oc new-app` | Create a new application | `oc new-app https://github.com/sclorg/cakephp-ex` |
| `oc get` | Displays one or many resources | `oc get pods` |
| `oc describe` | Show details of a specific resource or group of resources | `oc describe deployment myapp` |
| `oc delete` | Delete resources | `oc delete pod mypod` |
| `oc expose` | Expose a resource as a new OpenShift route | `oc expose service myapp` |
| `oc status` | Show an overview of the current project | `oc status` |

## Common Workflows

### Deploying a Docker container to Kubernetes
1. Build your Docker image: `docker build -t myapp:1.0 .`
2. Push the image to a registry: `docker push myregistry/myapp:1.0`
3. Create a Kubernetes deployment: `kubectl create deployment myapp --image=myregistry/myapp:1.0`
4. Expose the deployment: `kubectl expose deployment myapp --type=LoadBalancer --port=8080`

### Updating a Kubernetes deployment
1. Update your Docker image: `docker build -t myapp:1.1 .`
2. Push the new image: `docker push myregistry/myapp:1.1`
3. Update the deployment: `kubectl set image deployment/myapp myapp=myregistry/myapp:1.1`
4. Check rollout status: `kubectl rollout status deployment/myapp`

### Scaling a deployment
1. Scale up: `kubectl scale deployment myapp --replicas=5`
2. Check the status: `kubectl get pods`
3. Scale down: `kubectl scale deployment myapp --replicas=2`

### Rolling back a deployment
1. Check rollout history: `kubectl rollout history deployment/myapp`
2. Rollback to the previous version: `kubectl rollout undo deployment/myapp`
3. Verify the rollback: `kubectl rollout status deployment/myapp`

## Best Practices

1. Use meaningful tags for Docker images instead of `latest`.
2. Implement health checks in your Kubernetes deployments.
3. Use namespaces to organize resources in a Kubernetes cluster.
4. Regularly update and patch your container images.
5. Implement resource limits and requests for your containers.
6. Use ConfigMaps and Secrets to manage configuration separately from code.
7. Utilize Kubernetes liveness and readiness probes for better application reliability.
8. Implement proper logging and monitoring for your containers and clusters.
9. Use Helm charts for managing complex Kubernetes applications.
10. Practice GitOps for managing and deploying your infrastructure as code.

## Troubleshooting Tips

1. Check pod logs: `kubectl logs <pod-name>`
2. Describe a resource for detailed info: `kubectl describe <resource-type> <resource-name>`
3. Use port-forwarding for debugging: `kubectl port-forward <pod-name> 8080:80`
4. Check events in a namespace: `kubectl get events --sort-by=.metadata.creationTimestamp`
5. Exec into a container for interactive debugging: `kubectl exec -it <pod-name> -- /bin/bash`
6. Check node status: `kubectl get nodes`
7. Verify service endpoints: `kubectl get endpoints`
8. Review pod resource usage: `kubectl top pod`
9. Analyze network policies: `kubectl get networkpolicies`
10. Inspect persistent volume claims: `kubectl get pvc`

Remember to replace placeholders like `<pod-name>`, `myapp`, `myregistry`, etc., with your actual resource names when using these commands.
