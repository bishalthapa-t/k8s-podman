# Local Kubernetes Environment Setup With Podman 

This guide outlines how to set up a local Kubernetes environment using Podman and Minikube.

1. Install & Setup [podman](https://podman.io/)
   
   Podman is a container management tool developed by Red Hat that allows users to create, manage, and run container.
   It uses the OCI (Open Container Initiative) standard to manage containers, making it compatible with most container image formats, 
   meaning it can run containers created by other OCI-compliant tools, like Docker.

     - Install  ➤  `brew install podman`
     - Create linux virtual machine to run container  ➤  `podman machine init --memory=14000 --disk-size 100 trustly-local-k8s`
     - Start the virtual machine ➤  `podman machine start trustly-local-k8s`
     - Set the Podman connection to desired virtual machine (trustly-local-k8s) ➤ `podman system connection default trustly-local-k8s`
      - Restart Podman ➤  `podman machine stop trustly-local-k8s && podman machine start trustly-local-k8s` 
           

2. Install & Setup [minikube](https://minikube.sigs.k8s.io/docs/start/?arch=/macos/arm64/stable/binary+download)

   Minikube is a tool for running a single-node Kubernetes cluster locally. It creates a Kubernetes environment inside a container.
   It handles the complexities of installing and configuring Kubernetes components.
  
    - Install ➤ `brew install minikube`
    - Create kubernetes cluster ➤ `minikube --driver=podman --container-runtime=cri-o --memory=13000 --cpus=4 start`
    - Verify minikube is running ➤ `minikube status`


3. Install & Setup [kubectl](https://kubernetes.io/docs/reference/kubectl/)

   `kubectl` is the command-line tool used to interact with Kubernetes clusters.
   - Install  ➤ `brew install kubectl`
   - Configure to use local Minikube Kubernetes cluster  ➤ `kubectl config set-cluster minikube`


--- 
### Kubernetes Architecture & Core Component of K8s

- **[kube-apiserver](https://kubernetes.io/docs/concepts/architecture/#kube-apiserver)**: Entrypoint to K8s cluster
- **[kube-controller-manager](https://kubernetes.io/docs/concepts/architecture/#kube-controller-manager)**: Keeps track of what's happening in the cluster
- **[kube-scheduler](https://kubernetes.io/docs/concepts/architecture/#kube-scheduler)**: Ensures Pods placement
- **[kube-etcd](https://kubernetes.io/docs/concepts/architecture/#etcd)**: Kubernetes backing store for all cluster data

-- 

- **Pod**: Abstraction of container
- **Service**: communication
- **ConfigMap**, **Secret**: External configuration
- **Ingress**: route traffic into cluster
