# Kubectl cheat sheet

```bash
kubectl get pods
kubectl get pods -w
kubectl get svc
kubectl get nodes
kubectl logs <pod_name>
kubectl logs -f -l app=<service_name>
kubectl exec -it <pod_name> -- sh
kubectl describe node
kubectl port-forward <pod_name> <host_port>:<container_port>
```