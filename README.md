# EKS Application LoadBalancer Ingress Controller
**To Create Application LoadBalancer as Ingress Controller for EKS Cluster the below tags should be added to Private and Public Subnet of VPC of EKS Cluster.**
```
1. Public Subnets should be tagged with kubernetes.io/role/elb=1
2. Private Subnets should be tagged with kubernetes.io/role/internal-elb=1
```
<br><br/>
To Create EKS Cluster I have used Terraform script present in this repository.
