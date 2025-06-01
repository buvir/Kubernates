# Kubernates


***Kubernates Demo***
git branch -a


Give feedback
how to  start  single node kubernates contaniner very fast

To quickly start a single-node Kubernetes cluster using Docker Desktop, follow these steps:

Install Docker Desktop: Ensure you have the latest version of Docker Desktop installed on your machine. You can download it from the Docker Desktop page⁠.

Enable Kubernetes:

Open Docker Desktop.
Navigate to Settings.
Select the Kubernetes tab.
Check the box labeled Enable Kubernetes.
Click Apply & Restart.
This will set up a single-node Kubernetes cluster on your local machine. The setup time may vary depending on your internet speed as it needs to download necessary images.

Verify Kubernetes is Running:

Once Docker Desktop restarts, you can verify that Kubernetes is running by checking the Docker Desktop dashboard. You should see a green light indicating that Kubernetes is running.

Alternatively, you can use the command line to check the status:

```
kubectl get nodes
```
You should see an output similar to:

NAME             STATUS   ROLES           AGE   VERSION
docker-desktop   Ready    control-plane   5d    v1.30.2
This setup is designed for local development and testing, providing a convenient way to work with Kubernetes without needing a remote cluster. For more detailed instructions, you can refer to the Docker Desktop Kubernetes documentation⁠.

manual way in cmd prompt  intialise  minikube start and minikube status

If you're using Minikube to start a single-node Kubernetes cluster manually via the command prompt, here are the steps to do it quickly:

Install Minikube: Make sure Minikube is installed on your system. You can download it from the Minikube GitHub releases page⁠.
Start Minikube

Open your command prompt.

Run the following command to start Minikube:

```
minikube start

```
This command will start a local Kubernetes cluster. Minikube will automatically download the necessary images if they are not already present.

Check Minikube Status:

After starting Minikube, you can check its status with:

```
minikube status
```
This command will show you the status of the Minikube cluster and its components.

Verify Kubernetes is Running:

You can also verify that Kubernetes is running by using kubectl:
```
kubectl get nodes

```
You should see an output indicating that the Minikube node is ready.


do i have to do every time i using a startin a minkube becasue it consumes more space in my local

When you start Minikube, it creates a virtual machine or a container (depending on the driver you use) that runs the Kubernetes cluster. This can indeed consume a significant amount of disk space, especially if you frequently start and stop Minikube.

Here are some strategies to manage disk space usage with Minikube:

Delete Minikube Cluster When Not in Use:

If you're not using Minikube, you can delete the cluster to free up space:
```
minikube delete

```
This command removes the Minikube VM or container, freeing up the space it was using.

Use Minikube Profiles:

Minikube supports profiles, which allow you to manage multiple clusters. You can create a new profile for different projects and delete them when not needed:
```
minikube start -p myprofile
minikube delete -p myprofile
```
Use a Lightweight Base Image:

Minikube allows you to specify a base image. Using a lightweight image can reduce the space used:
```
minikube start --base-image=gcr.io/k8s-minikube/kicbase:v0.0.30
```
Regularly Prune Docker Resources:

If you're using Docker as the driver, regularly prune unused Docker resources to free up space:
```
docker system prune -f
```
Check Disk Usage:

You can check how much space Minikube is using with:
```
minikube ssh -- df -h
```
By following these practices, you can manage the disk space usage of Minikube more effectively. If you find that Minikube is still consuming too much space, consider using a cloud-based Kubernetes service for development and testing, which offloads the resource usage from your local machine.

#### K8s manifest files 
* mongo-config.yaml
* mongo-secret.yaml
* mongo.yaml
* webapp.yaml

#### K8s commands

##### start Minikube and check status
    minikube start --vm-driver=hyperkit 
    minikube status

##### get minikube node's ip address
    minikube ip

##### get basic info about k8s components
    kubectl get node
    kubectl get pod
    kubectl get svc
    kubectl get all

##### get extended info about components
    kubectl get pod -o wide
    kubectl get node -o wide

##### get detailed info about a specific component
    kubectl describe svc {svc-name}
    kubectl describe pod {pod-name}

##### get application logs
    kubectl logs {pod-name}
    
##### stop your Minikube cluster
    minikube stop

<br />

> :warning: **Known issue - Minikube IP not accessible** 

If you can't access the NodePort service webapp with `MinikubeIP:NodePort`, execute the following command:
    
    minikube service webapp-service

<br />

#### Links
* mongodb image on Docker Hub: https://hub.docker.com/_/mongo
* webapp image on Docker Hub: https://hub.docker.com/repository/docker/nanajanashia/k8s-demo-app
* k8s official documentation: https://kubernetes.io/docs/home/
* webapp code repo: https://gitlab.com/nanuchi/developing-with-docker/-/tree/feature/k8s-in-hour
