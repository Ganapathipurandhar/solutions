# Kubernetes Crash Recovery and Debugging Commands

This document contains a comprehensive list of Kubernetes commands for crash recovery, debugging, and general cluster management.

---

## Pod Management

1. **`kubectl get pods --all-namespaces`**: List all pods across all namespaces.
2. **`kubectl describe pod <pod_name>`**: Get detailed information about a specific pod.
3. **`kubectl logs <pod_name> -c <container_name>`**: View logs of a specific container in a pod.
4. **`kubectl delete pod <pod_name> --grace-period=0 --force`**: Forcefully delete a pod.
5. **`kubectl exec -it <pod_name> -- /bin/sh`**: Open a shell inside a running container for debugging.
6. **`kubectl cp <pod_name>:/path/to/file /local/path`**: Copy files from a pod to your local machine.
7. **`kubectl get pods -o wide`**: List pods with additional details like node and IP.
8. **`kubectl get pods --field-selector=status.phase=Running`**: List only running pods.

---

## Deployment and Rollout Management

9. **`kubectl rollout undo deployment <deployment_name>`**: Roll back a deployment to the previous version.
10. **`kubectl rollout status deployment <deployment_name>`**: Check the status of a deployment rollout.
11. **`kubectl rollout history deployment <deployment_name>`**: View the rollout history of a deployment.
12. **`kubectl scale deployment <deployment_name> --replicas=<number>`**: Scale a deployment up or down.
13. **`kubectl set image deployment/<deployment_name> <container_name>=<new_image>`**: Update the image of a container in a deployment.

---

## Node Management

14. **`kubectl get nodes`**: List all nodes in the cluster.
15. **`kubectl describe node <node_name>`**: Get detailed information about a specific node.
16. **`kubectl drain <node_name> --ignore-daemonsets`**: Safely drain a node for maintenance.
17. **`kubectl cordon <node_name>`**: Mark a node as unschedulable.
18. **`kubectl uncordon <node_name>`**: Mark a node as schedulable again.
19. **`kubectl taint nodes <node_name> <key>=<value>:NoSchedule`**: Add a taint to a node to prevent scheduling.
20. **`kubectl top nodes`**: Monitor resource usage (CPU/memory) of nodes.

---

## Service and Endpoint Management

21. **`kubectl get services`**: List all services in the current namespace.
22. **`kubectl get endpoints <service_name>`**: List endpoints for a specific service.
23. **`kubectl expose deployment <deployment_name> --type=LoadBalancer --port=<port>`**: Expose a deployment as a service.
24. **`kubectl get ingress`**: List all ingress resources.

---

## Cluster and Component Health

25. **`kubectl get componentstatuses`**: Check the health of core cluster components (e.g., etcd, kube-apiserver).
26. **`kubectl get events --all-namespaces --sort-by=.metadata.creationTimestamp`**: View cluster events sorted by creation time.
27. **`kubectl cluster-info`**: Display cluster information and health.
28. **`kubectl get csr`**: List Certificate Signing Requests (useful for debugging node registration).

---

## Resource Monitoring

29. **`kubectl top pods --all-namespaces`**: Monitor resource usage of pods across all namespaces.
30. **`kubectl top nodes`**: Monitor resource usage of nodes.
31. **`kubectl get hpa`**: List Horizontal Pod Autoscalers (HPA) and their status.

---

## Configuration and Debugging

32. **`kubectl apply -f <file.yaml>`**: Apply a configuration from a YAML file.
33. **`kubectl delete -f <file.yaml>`**: Delete resources defined in a YAML file.
34. **`kubectl edit deployment <deployment_name>`**: Edit a deployment in place.
35. **`kubectl config view`**: View the current Kubernetes configuration.
36. **`kubectl config use-context <context_name>`**: Switch to a different Kubernetes context.
37. **`kubectl auth can-i <verb> <resource>`**: Check if you have permission to perform an action.

---

## Namespace Management

38. **`kubectl get namespaces`**: List all namespaces.
39. **`kubectl create namespace <namespace_name>`**: Create a new namespace.
40. **`kubectl delete namespace <namespace_name>`**: Delete a namespace.
41. **`kubectl config set-context --current --namespace=<namespace_name>`**: Switch to a specific namespace.

---

## ETCD and Backup Management

42. **`etcdctl --endpoints=https://<etcd-server>:2379 snapshot save backup.db`**: Take a snapshot of the etcd database.
43. **`etcdctl --endpoints=https://<etcd-server>:2379 snapshot restore backup.db`**: Restore etcd from a snapshot.
44. **`kubectl get secrets`**: List all secrets in the current namespace.

---

## Miscellaneous

45. **`kubectl get pv`**: List Persistent Volumes (PV).
46. **`kubectl get pvc`**: List Persistent Volume Claims (PVC).
47. **`kubectl get storageclass`**: List storage classes.
48. **`kubectl get jobs`**: List all jobs.
49. **`kubectl get cronjobs`**: List all cron jobs.
50. **`kubectl get configmaps`**: List all ConfigMaps in the current namespace.

---

This list covers a wide range of scenarios, from debugging and recovery to general cluster management. Save this as a `.md` file for quick reference!