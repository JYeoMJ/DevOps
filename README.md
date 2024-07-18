# Comprehensive DevOps Cheat Sheet: Docker, Kubernetes, and OpenShift

## Table of Contents
1. [Containers & Containerization](#containers--containerization)
2. [Docker CLI](#docker-cli)
3. [Introduction to Kubernetes](#introduction-to-kubernetes)
4. [Kubernetes Architecture](#kubernetes-architecture)
5. [Managing Applications with Kubernetes](#managing-applications-with-kubernetes)
6. [The Kubernetes Ecosystem: OpenShift, Istio, etc](#the-kubernetes-ecosystem-openshift-istio-etc)
7. [OpenShift CLI](#openshift-cli)
8. [Common Workflows](#common-workflows)
9. [Best Practices](#best-practices)
10. [Troubleshooting Tips](#troubleshooting-tips)

## Containers & Containerization

A container is a unit of software that encapsulates everything needed to build, ship, and run applications.  

- Containers lower deployment time and costs, improve utilization, automate processes, and support next-gen applications (microservices).
- Major container vendors include Docker, Podman, LXC, and Vagrant. 
- Docker is an open platform used for developing, shipping, and running applications as containers. 
- Docker containers are not a good fit for applications based on monolithic architecture or applications that require high performance or security. 

### Docker Architecture
- Consists of the Docker client, the Docker host, and the container registry. 
- The Docker host contains objects such as the Dockerfiles, images, containers, networks, storage volumes, and other objects, such as plugins and add-ons. 
- Docker uses networks to isolate container communications. 
- Docker uses volumes and binds mounts to persist data even after a container stops running. 
- Plugins, such as storage plugins, provide the ability to connect to external storage platforms. 

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

## Introduction to Kubernetes

Container orchestration automates the container lifecycle resulting in faster deployments, reduced errors, higher availability, and more robust security. 

Kubernetes is a highly portable, horizontally scalable, open-source container orchestration system with automated deployment and simplified management capabilities.  

### Kubernetes Architecture
- Consists of a control plane and one or more worker planes. 
- A control plane includes controllers, an API server, a scheduler, and an etcd. 
- A worker plane includes nodes, a kubelet, container runtime, and kube-proxy. 

### Kubernetes Objects
- Include Namespaces, Pods, ReplicaSets, Deployments, and Services. 
- Namespaces help in isolating groups of resources within a single cluster. 
- Pods represent a process or an instance of an app running in the cluster. 
- ReplicaSets create and manage horizontally scaled running Pods. 
- Deployments provide updates for Pods and ReplicaSets. 
- A service in Kubernetes is a REST object that provides policies for accessing the pods and cluster. 

### Kubernetes Capabilities
Include automated rollouts and rollbacks, storage orchestration, horizontal scaling, automated bin packing, secret and configuration management, Ipv4/Ipv6 dual-stack support, batch execution, self-healing, service discovery, load balancing, and extensible design. 

### Kubernetes Services
- ClusterIP provides Inter-service communication within the cluster
- NodePort Service creates and routes the incoming requests automatically to the ClusterIP Service
- External Load Balancer, or ELB, creates NodePort and ClusterIP Services automatically
- External Name service represents external storage and enables Pods from different namespaces to talk to each other

### Additional Kubernetes Concepts
- Ingress is an API object that provides routing rules to manage external users' access to multiple services in a Kubernetes cluster
- DaemonSet ensures that there is at least one copy of the pod on all nodes
- StatefulSet manages stateful applications, manages Pod deployment and scaling, maintains a sticky identity for each Pod request and provides persistent storage volumes for your workloads
- Job creates pods and tracks the Pod completion process; Jobs are retried until completed

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

- A ReplicaSet enables scaling by creating or deleting pods. 
- A ReplicaSet always tries to match the actual state to the desired state. 
- Autoscaling enables scaling as needed at the cluster or node level, and the pod level. 
- Autoscaler types include horizontal pod (HPA), vertical pod (VPA), and cluster (CA).
- Rolling updates roll out app changes in a controlled and automated way. 
- Rolling updates and rollback can be performed using all-at-once and one-at-a-time strategies. 
- ConfigMaps are used to provide variables for your application. 
- Secrets are used to provide sensitive information to your application. 
- Binding an external Service to your deployment automatically provides the credentials to use the Service inside the code. 
- Binding manages configuration and credentials for back-end Services while protecting sensitive data. 

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

## The Kubernetes Ecosystem: OpenShift, Istio, etc

### OpenShift
- OpenShift® is an enterprise-ready Kubernetes container platform built for open hybrid cloud.
- OpenShift is easier to use, integrates with Jenkins, and has more services and features.

### Custom Resources and Operators
- Custom resource definitions (CRDs) extend the Kubernetes API. 
- CRDs paired with custom controllers create new, declarative APIs in Kubernetes. 
- Operators use CRDs and custom controllers to automate cluster tasks. 

### OpenShift-specific Concepts
- A build is a process that transforms inputs into an object. 
- An ImageStream is an abstraction for referencing container images in OpenShift. 

### Service Mesh and Istio
- A service mesh provides traffic management to control the flow of traffic between services, security to encrypt traffic between services, and observability of service behavior to troubleshoot and optimize applications. 
- Istio is a service mesh that supports four concepts of connection, security, enforcement, and observability. It is commonly used with Microservices applications. 
- Istio provides service communication metrics for basic service monitoring needs: latency, traffic, errors, and saturation. 

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
