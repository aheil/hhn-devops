# Lab 08 - Kubernetes 
## Task 1 - Minikube 

### Mindestvoraussetzung für diese Übung 
* 2 CPUs 
* 2GB free memory 
* ~20GB free disk space
* One of the following container or virtualizing technologies
   * [Hyperkit](https://minikube.sigs.k8s.io/docs/drivers/hyperkit/)
   * [Hyper-V](https://minikube.sigs.k8s.io/docs/drivers/hyperv/)
   * [KVM2](https://minikube.sigs.k8s.io/docs/drivers/kvm2/)
    * [Docker](https://minikube.sigs.k8s.io/docs/drivers/docker/)
    * [Podman](https://minikube.sigs.k8s.io/docs/drivers/podman/) 
    * [Parallels](https://minikube.sigs.k8s.io/docs/drivers/parallels/)
    * [VirtualBox](https://minikube.sigs.k8s.io/docs/drivers/virtualbox/)
    * [VMWare](https://minikube.sigs.k8s.io/docs/drivers/vmware/)
* [winget](https://github.com/microsoft/winget-cli) (Windows Package Manager Client) 

1. Install Minikube via `winget install minicube`
2. Verify the successful installation via `minikube version` and `kubectl version`
3. Start the cluster via `minikube start` 
4. Check the status of your cluster via  `kubectl get po -A`
5. Start the Kubernetes dashboard via `kubernetes dashboard`
6. Create an example deployment via `kubectl create deploymenthello-minikube --image=k8s.gcr.io/echoserver:1.4`
7. Expose port 8080 for your deployment using `kubectl expose deploymenthello-minikube --type=NodePort --port=8080`
8. Check the status of your deployment `kubectl get serviceshello-minikube`
9. Vie your service status in your standard browser to get an overview of your service `minikube service hello-minikube`
10. Pause the cluster without changing the deployments via`minikube pause`
11. Stop the cluster `minikube stop`
12. Change the available memory  `minikubeconfig set memory 16384`
13. Delete your cluster `minikube delete --all` 

