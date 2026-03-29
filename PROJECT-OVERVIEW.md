# Multi-Node Kubernetes Deployment on Azure
A hands-on DevOps project demonstrating the deployment, networking, and resilience of a Kubernetes cluster on Microsoft Azure.## Overview
This project demonstrates the design, deployment, and validation of a multi-node Kubernetes cluster on Microsoft Azure using kubeadm and Ansible.
## Objective
Design, deploy, and validate a multi-node Kubernetes cluster on Microsoft Azure, expose a sample workload externally, and demonstrate:
- Multi-node scheduling
- Inter-node networking
- External service exposure
- Operational resilience under failure scenarios
## Technologies Used
- Microsoft Azure
- Kubernetes (kubeadm)
- Ansible
- Calico (CNI)
- containerd
- Linux (Ubuntu)## Architecture
- Platform: Microsoft Azure
- Region: North Europe
- OS: Ubuntu 24.04 LTS
- Container Runtime: containerd
- CNI: Calico
- Provisioning: Ansible + kubeadm

## Cluster Topology
- gtvm1 – Control Plane – 172.16.0.4
- gtvm3 – Worker – 172.16.0.5

Both nodes were deployed into the same Azure Virtual Network and subnet.

## Cluster Bootstrap
- Initialised the cluster with kubeadm
- Configured kubeconfig for cluster administration
- Installed Calico CNI for pod networking
- Joined the worker node using kubeadm join

## Validation
The cluster was validated through:
- `kubectl get nodes`
- pod scheduling checks
- external NodePort connectivity tests
- drain and failover simulation

## Service Exposure
- Service Type: NodePort
- Port: 30080/TCP
- Azure NSG rule added to allow inbound TCP 30080

## Resilience Testing
- Pod recreation after deletion
- Node drain and workload rescheduling
- Service remained accessible during failover

## Production Considerations
This project used a single control plane, which introduces a single point of failure. A production-grade design would use:
- 3 or more control-plane nodes
- quorum-based etcd
- internal load balancing
- better capacity planning
