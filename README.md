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

## k9s commands
```
:service
:namespace
:service
:deployment
```
