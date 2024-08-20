## Amazon Kubernetes Cluster Architecture - Foundational Setup

In order to build a house , you must draw the building architecture first , so is creating a K8S cluster , the following describes the pillars in which you should pay respect in order to create a strong K8S cluster


1. **Networking Components:**
   - Established Virtual Private Cloud (VPC) with subnets, route tables, internet gateway, and NAT gateway.
  
2. **Security Measures:**
   - Configured security groups, IAM roles, policies, and network ACLs to ensure secure access and control.
  
3. **Compute Resources:**
   - Launched EC2 instances, set up Auto Scaling Groups for scalability, and attached Elastic Block Store (EBS) volumes for persistent storage.
  
4. **Storage Solutions:**
   - Integrated S3 buckets for backups and logs, with potential consideration of Elastic File System (EFS) for shared storage needs.
  
5. **DNS and Load Balancing:**
   - Deployed an Elastic Load Balancer (ELB) and configured Route 53 for efficient traffic management and DNS resolution.

After some deep research i was able to create an architecture for deploying my K8S cluster :

![Kubernetes Cluster Architecture](pictures\pic.png)   
<p align="center"><i>Figure 1: Diagram of the Amazon Kubernetes Cluster Architecture</i></p>         

Here is a breakdown of each component and its function :
## **Kubernetes Cluster Architecture Overview**

This document provides an overview of the key components involved in setting up a Kubernetes cluster on Amazon Web Services (AWS) using Elastic Kubernetes Service (EKS).

### **1. VPC (Virtual Private Cloud)**
- **Purpose:** The VPC is the isolated network environment where all resources in your Kubernetes cluster reside. It provides a virtual network that you define and manage.

### **2. Public Subnet**
- **Purpose:** This subnet is a segment within your VPC that is publicly accessible from the internet. Resources in this subnet, such as the load balancer, can communicate directly with the internet.

### **3. Private Subnet**
- **Purpose:** This subnet is a segment within your VPC that is not directly accessible from the internet. It hosts your EKS control plane and worker nodes, providing an extra layer of security.

### **4. Internet Gateway**
- **Purpose:** The Internet Gateway enables instances within your VPC to connect to the internet and allows the public subnet to route traffic to and from the internet.

### **5. Route 53**
- **Purpose:** Route 53 is Amazon's DNS service. It routes end-user traffic to the appropriate resources, such as the load balancer, based on domain names.

### **6. Elastic Load Balancer (ELB)**
- **Purpose:** The ELB distributes incoming traffic across your EC2 instances (worker nodes) within the private subnet, ensuring high availability and fault tolerance.

### **7. S3 Bucket**
- **Purpose:** Amazon S3 is a storage service used to store data such as backups, logs, and other artifacts. In this architecture, it might be used for storing cluster-related data.

### **8. EKS Control Management Plane**
- **Components:**
  - **etcd:** Stores the state of the Kubernetes cluster.
  - **API Server:** The front-end for the Kubernetes control plane, handling all REST requests.
  - **Scheduler:** Schedules pods to run on specific nodes.
  - **Controller Manager:** Manages controllers that regulate the state of the cluster.
- **Purpose:** The EKS control plane manages the overall operations of the Kubernetes cluster. It's fully managed by AWS in EKS, meaning you don't need to maintain it yourself.

### **9. Worker Nodes (EC2 Instances)**
- **Purpose:** These are EC2 instances that run your Kubernetes pods. They handle the workload and communicate with the control plane to manage pod deployment and scaling.

### **10. Pods**
- **Purpose:** Pods are the smallest deployable units in Kubernetes. They encapsulate your application containers and run on the worker nodes.

### **11. kubectl**
- **Purpose:** `kubectl` is the command-line tool used to interact with the Kubernetes API server. It allows you to manage and inspect the Kubernetes cluster's resources.

### **12. KMS (Key Management Service) API**
- **Purpose:** The KMS API in this context is likely used for managing encryption keys that secure sensitive data within the Kubernetes cluster.

