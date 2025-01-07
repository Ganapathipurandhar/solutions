# Minikube Start Options Documentation

This document provides a comprehensive list of options for starting and configuring Minikube clusters.

1. Resource Allocation Options

These options allow you to control how much CPU, memory, and disk space Minikube uses:

1.1 CPUs

Flag: --cpus

Description: Set the number of CPUs allocated to the Minikube VM.

Example:
~~~
minikube start --cpus=2
~~~
Allocate 2 CPUs to Minikube.

1.2 Memory

Flag: --memory

Description: Set the amount of memory (RAM) allocated to the Minikube VM.

Example:
~~~
minikube start --memory=4096
~~~
Allocate 4 GB of RAM.

1.3 Disk Size

Flag: --disk-size

Description: Set the disk space for the Minikube VM.

Example:
~~~
minikube start --disk-size=20g
~~~
Allocate 20 GB of disk space.

2. Driver Options

These options specify the driver to run Minikube.

2.1 Driver Selection

Flag: --driver

Description: Specify the driver for Minikube.

Options:

virtualbox

docker

hyperv

Example:
~~~
minikube start --driver=docker
~~~
2.2 Skip Virtualization Check

Flag: --no-vtx-check

Description: Skip the VT-x/AMD-v virtualization check.

Example:
~~~
minikube start --driver=virtualbox --no-vtx-check
~~~
3. Cluster Configuration Options

These options allow you to customize your Minikube cluster.

3.1 Kubernetes Version

Flag: --kubernetes-version

Description: Specify the Kubernetes version for the cluster.

Example:
~~~
minikube start --kubernetes-version=v1.28.0
~~~
3.2 Multi-Node Clusters

Flag: --nodes

Description: Create a multi-node (multi-control plane) cluster.

Example:
~~~
minikube start --nodes=3
~~~
Create a cluster with 3 nodes.

3.3 Addons

Flag: --addons

Description: Enable specific Minikube addons during cluster creation.

Common Addons:

dashboard

metrics-server

ingress

Example:
~~~
minikube start --addons=dashboard,metrics-server
~~~
4. Networking Options

4.1 Port Exposing

Flag: --ports

Description: Expose specific ports from the Minikube VM to your host.

Example:
~~~
minikube start --ports=8080:80
~~~
4.2 API Server Port

Flag: --apiserver-port

Description: Set the port for the Kubernetes API server.

Example:
~~~
minikube start --apiserver-port=8443
~~~
4.3 Extra Configurations

Flag: --extra-config

Description: Pass additional configuration to Kubernetes components.

Example:
~~~
minikube start --extra-config=kubelet.max-pods=110
~~~
5. Performance Tuning Options

5.1 CNI (Container Network Interface)

Flag: --cni

Description: Choose a Container Network Interface plugin.

Example:
~~~
minikube start --cni=flannel
~~~
5.2 Container Runtime

Flag: --container-runtime

Description: Choose the container runtime for Kubernetes.

Options:

docker

containerd

cri-o

Example:
~~~
minikube start --container-runtime=containerd
~~~
6. Debugging Options

6.1 Verbosity

Flag: --v

Description: Set the verbosity level for logs.

Example:
~~~
minikube start --v=3
~~~
6.2 Log File

Flag: --log-file

Description: Save logs to a file for later inspection.

Example:
~~~
minikube start --log-file=minikube.log
~~~
6.3 Dry Run

Flag: --dry-run

Description: Simulate the Minikube start process without making actual changes.

Example:
~~~
minikube start --dry-run
~~~
Example Command

# Here is an example command with multiple options combined:
~~~
minikube start --driver=virtualbox --memory=4096 --cpus=2 --disk-size=20g --kubernetes-version=v1.28.0 --addons=dashboard,metrics-server
~~~
This document covers the most common options for configuring Minikube. Let me know if you'd like additional information or assistance with a specific setup!

