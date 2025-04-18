# Kubernetes knowledge

## Download
https://docs.docker.com/desktop/setup/install/mac-install/
https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/#install-with-homebrew-on-macos
https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Farm64%2Fstable%2Fhomebrew
https://github.com/derailed/k9s

## Tutorial
https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro/
https://kubernetes.io/docs/tutorials/hello-minikube/

## Get Started summary
```
1. start docker

2. create minikube cluster in local
minikube start

3. Kubernetes dashboard
minikube dashboard

4. create deployment
kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
kubectl get deployments
kubectl get pods
kubectl get events
kubectl config view
kubectl logs hello-node-*

5. create service
kubectl expose deployment hello-node --type=LoadBalancer --port=8080
kubectl get services

6. view service --> access localhost 50301 --> tunnel to node/vm 192.168.49.2:32128 --> map to service 8080
minikube service hello-node
|-----------|------------|-------------|---------------------------|
| NAMESPACE |    NAME    | TARGET PORT |            URL            |
|-----------|------------|-------------|---------------------------|
| default   | hello-node |        8080 | http://192.168.49.2:32128 |
|-----------|------------|-------------|---------------------------|
🏃  Starting tunnel for service hello-node.
|-----------|------------|-------------|------------------------|
| NAMESPACE |    NAME    | TARGET PORT |          URL           |
|-----------|------------|-------------|------------------------|
| default   | hello-node |             | http://127.0.0.1:50301 |
|-----------|------------|-------------|------------------------|
🎉  Opening service default/hello-node in default browser...

7. addons
minikube addons list
minikube addons enable metrics-server
kubectl get pod,svc -n kube-system
kubectl top pods
minikube addons disable metrics-server

8. clean up
kubectl delete service hello-node
kubectl delete deployment hello-node
minikube stop
# Optional
minikube delete
```

## Commands
```
print env variables
kubectl exec "$POD_NAME" -- env

bash session
kubectl exec -ti $POD_NAME -- bash
```

## k9s commands
```
:context
:namespace
:service
:deployment
```

## Concepts

### Node
1. worker machine, virtual or physical
2. managed by control plane
3. can have multiple pods
4. Kubelet --> communication with control plane
5. container runtime (e.g. Docker)

### Pod
1. \>= 1 app containers
2. with shared storage volumes, IP and info on how to run each container
3. models an app-specific logical host
4. should contain tightly-coupled app containers
5. run in isolated private network
6. `kubectl proxy` --> expose network
7. `curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME:8080/proxy/`
