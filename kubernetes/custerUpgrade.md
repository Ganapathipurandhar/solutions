# Upgrading Kubernetes Cluster:

### Overview

This document outlines the steps to safely and efficiently upgrade a Kubernetes cluster in a company environment. The upgrade process includes updating the control plane, worker nodes, and verifying the stability of the cluster post-upgrade. These steps ensure minimal downtime and compatibility with existing workloads.

### Prerequisites

Backup and Disaster Recovery:

Etcd Backup:

For clusters using etcd as the key-value store, take a snapshot using the following command:
~~~
ETCDCTL_API=3 etcdctl snapshot save <backup-file> \
  --endpoints=<etcd-endpoint> \
  --cert=<etcd-cert-file> \
  --key=<etcd-key-file> \
  --cacert=<etcd-cacert-file>
~~~
Verify the snapshot:
~~~
ETCDCTL_API=3 etcdctl snapshot status <backup-file>
~~~
Cluster Configuration Backup:

Export all Kubernetes objects:
~~~
kubectl get all --all-namespaces -o yaml > cluster-backup.yaml
~~~
Backup resource-specific configurations such as PVs, PVCs, and ConfigMaps as needed.

Cluster Health Check:

Verify all nodes and pods are healthy using kubectl get nodes and kubectl get pods --all-namespaces.

Address any pending issues before proceeding.

Compatibility Check:

Review release notes for the new Kubernetes version.

Ensure all addons, plugins, and custom workloads are compatible with the target version.

Access:

Ensure you have admin-level access to the cluster and cloud provider (if applicable).

Upgrade Steps

1. Plan the Upgrade

Identify the current Kubernetes version using:
~~~
kubectl version --short
~~~
Determine the desired target version. Follow the version skew policy: upgrade only one minor version at a time (e.g., 1.24 to 1.25).

Schedule maintenance windows for minimal disruption.

2. Upgrade Control Plane

a. Managed Kubernetes Service (e.g., EKS, AKS, GKE):

Use the cloud provider’s CLI or console to upgrade the control plane.

Example for AKS:
~~~
az aks upgrade --resource-group <resource-group> --name <cluster-name> --kubernetes-version <target-version>
~~~
Verify the upgrade:
~~~
kubectl get nodes
~~~
b. Self-Managed Kubernetes Cluster:

Upgrade kubeadm:

sudo apt-get update && sudo apt-get install -y kubeadm=<target-version>

Upgrade the control plane:

sudo kubeadm upgrade apply <target-version>

Update kubelet and kubectl:

sudo apt-get install -y kubelet=<target-version> kubectl=<target-version>
sudo systemctl restart kubelet

3. Upgrade Worker Nodes

a. Cordoning and Draining Nodes:

Cordon the node to prevent new workloads:

kubectl cordon <node-name>

Drain the node:

kubectl drain <node-name> --ignore-daemonsets --delete-emptydir-data

b. Update Node Software:

Upgrade kubeadm on the node:

sudo apt-get install -y kubeadm=<target-version>
sudo kubeadm upgrade node

Upgrade kubelet and kubectl:

sudo apt-get install -y kubelet=<target-version> kubectl=<target-version>
sudo systemctl restart kubelet

c. Uncordoning Nodes:

Allow the node to accept workloads:

kubectl uncordon <node-name>

4. Verify Cluster Health

Confirm all nodes are upgraded:

kubectl get nodes

Check the status of workloads:

kubectl get pods --all-namespaces

Run conformance tests (optional) to validate functionality.

Post-Upgrade Steps

Update Addons and Plugins:

Upgrade CNI plugins, ingress controllers, and other tools.

Monitor the Cluster:

Use tools like Prometheus, Grafana, or the cloud provider’s monitoring solution to ensure stability.

Documentation:

Update the documentation with the new cluster version and changes.

Rollback Plan

In case of failure:

Revert to the backup taken before the upgrade.

Downgrade to the previous Kubernetes version using the appropriate tools or cluster snapshots.

Conclusion

Follow this procedure for a structured and safe Kubernetes upgrade. Testing in a staging environment before production upgrades is highly recommended to ensure compatibility and minimize risks.