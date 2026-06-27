Install Minikube

https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download
minikube start --driver=docker

install Kubectl
https://kubernetes.io/docs/tasks/tools/

Kubectl autocomplete
kubectl completion -h
https://kubernetes.io/docs/reference/kubectl/generated/kubectl_completion/



kubectl port-forward svc/hello-k8s 8080:80


# Check tools
docker --version
minikube version
kubectl version --client

# Start local Kubernetes
minikube start

# Inspect cluster
kubectl get nodes
kubectl cluster-info
kubectl get pods -A

# Create first deployment
kubectl create deployment hello-k8s --image=nginx

# Inspect app
kubectl get deployments
kubectl get pods

# Scale app
kubectl scale deployment hello-k8s --replicas=3
kubectl get pods

# Expose app
kubectl expose deployment hello-k8s --type=NodePort --port=80
kubectl get services

# Open service
minikube service hello-k8s

# Apply declarative YAML
kubectl apply -f manifests/
kubectl get deployments
kubectl get pods
kubectl get svc
minikube service hello-k8s-yaml

# Clean up imperative resources
kubectl delete deployment hello-k8s
kubectl delete service hello-k8s

# Clean up declarative resources
kubectl delete -f manifests/

# Stop or delete local cluster
minikube stop
minikube delete
