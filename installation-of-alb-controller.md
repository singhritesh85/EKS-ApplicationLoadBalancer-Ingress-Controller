1. Create IAM Policy with the Name **AWSLoadBalancerControllerIAMPolicy** using below mentioned json.
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:CreateServiceLinkedRole"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "iam:AWSServiceName": "elasticloadbalancing.amazonaws.com"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeAccountAttributes",
                "ec2:DescribeAddresses",
                "ec2:DescribeAvailabilityZones",
                "ec2:DescribeInternetGateways",
                "ec2:DescribeVpcs",
                "ec2:DescribeVpcPeeringConnections",
                "ec2:DescribeSubnets",
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeInstances",
                "ec2:DescribeNetworkInterfaces",
                "ec2:DescribeTags",
                "ec2:GetCoipPoolUsage",
                "ec2:DescribeCoipPools",
                "elasticloadbalancing:DescribeLoadBalancers",
                "elasticloadbalancing:DescribeLoadBalancerAttributes",
                "elasticloadbalancing:DescribeListeners",
                "elasticloadbalancing:DescribeListenerCertificates",
                "elasticloadbalancing:DescribeSSLPolicies",
                "elasticloadbalancing:DescribeRules",
                "elasticloadbalancing:DescribeTargetGroups",
                "elasticloadbalancing:DescribeTargetGroupAttributes",
                "elasticloadbalancing:DescribeTargetHealth",
                "elasticloadbalancing:DescribeTags",
                "elasticloadbalancing:DescribeTrustStores"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "cognito-idp:DescribeUserPoolClient",
                "acm:ListCertificates",
                "acm:DescribeCertificate",
                "iam:ListServerCertificates",
                "iam:GetServerCertificate",
                "waf-regional:GetWebACL",
                "waf-regional:GetWebACLForResource",
                "waf-regional:AssociateWebACL",
                "waf-regional:DisassociateWebACL",
                "wafv2:GetWebACL",
                "wafv2:GetWebACLForResource",
                "wafv2:AssociateWebACL",
                "wafv2:DisassociateWebACL",
                "shield:GetSubscriptionState",
                "shield:DescribeProtection",
                "shield:CreateProtection",
                "shield:DeleteProtection"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:AuthorizeSecurityGroupIngress",
                "ec2:RevokeSecurityGroupIngress"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:CreateSecurityGroup"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:CreateTags"
            ],
            "Resource": "arn:aws:ec2:*:*:security-group/*",
            "Condition": {
                "StringEquals": {
                    "ec2:CreateAction": "CreateSecurityGroup"
                },
                "Null": {
                    "aws:RequestTag/elbv2.k8s.aws/cluster": "false"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:CreateTags",
                "ec2:DeleteTags"
            ],
            "Resource": "arn:aws:ec2:*:*:security-group/*",
            "Condition": {
                "Null": {
                    "aws:RequestTag/elbv2.k8s.aws/cluster": "true",
                    "aws:ResourceTag/elbv2.k8s.aws/cluster": "false"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:AuthorizeSecurityGroupIngress",
                "ec2:RevokeSecurityGroupIngress",
                "ec2:DeleteSecurityGroup"
            ],
            "Resource": "*",
            "Condition": {
                "Null": {
                    "aws:ResourceTag/elbv2.k8s.aws/cluster": "false"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:CreateLoadBalancer",
                "elasticloadbalancing:CreateTargetGroup"
            ],
            "Resource": "*",
            "Condition": {
                "Null": {
                    "aws:RequestTag/elbv2.k8s.aws/cluster": "false"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:CreateListener",
                "elasticloadbalancing:DeleteListener",
                "elasticloadbalancing:CreateRule",
                "elasticloadbalancing:DeleteRule"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:AddTags",
                "elasticloadbalancing:RemoveTags"
            ],
            "Resource": [
                "arn:aws:elasticloadbalancing:*:*:targetgroup/*/*",
                "arn:aws:elasticloadbalancing:*:*:loadbalancer/net/*/*",
                "arn:aws:elasticloadbalancing:*:*:loadbalancer/app/*/*"
            ],
            "Condition": {
                "Null": {
                    "aws:RequestTag/elbv2.k8s.aws/cluster": "true",
                    "aws:ResourceTag/elbv2.k8s.aws/cluster": "false"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:AddTags",
                "elasticloadbalancing:RemoveTags"
            ],
            "Resource": [
                "arn:aws:elasticloadbalancing:*:*:listener/net/*/*/*",
                "arn:aws:elasticloadbalancing:*:*:listener/app/*/*/*",
                "arn:aws:elasticloadbalancing:*:*:listener-rule/net/*/*/*",
                "arn:aws:elasticloadbalancing:*:*:listener-rule/app/*/*/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:ModifyLoadBalancerAttributes",
                "elasticloadbalancing:SetIpAddressType",
                "elasticloadbalancing:SetSecurityGroups",
                "elasticloadbalancing:SetSubnets",
                "elasticloadbalancing:DeleteLoadBalancer",
                "elasticloadbalancing:ModifyTargetGroup",
                "elasticloadbalancing:ModifyTargetGroupAttributes",
                "elasticloadbalancing:DeleteTargetGroup"
            ],
            "Resource": "*",
            "Condition": {
                "Null": {
                    "aws:ResourceTag/elbv2.k8s.aws/cluster": "false"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:AddTags"
            ],
            "Resource": [
                "arn:aws:elasticloadbalancing:*:*:targetgroup/*/*",
                "arn:aws:elasticloadbalancing:*:*:loadbalancer/net/*/*",
                "arn:aws:elasticloadbalancing:*:*:loadbalancer/app/*/*"
            ],
            "Condition": {
                "StringEquals": {
                    "elasticloadbalancing:CreateAction": [
                        "CreateTargetGroup",
                        "CreateLoadBalancer"
                    ]
                },
                "Null": {
                    "aws:RequestTag/elbv2.k8s.aws/cluster": "false"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:RegisterTargets",
                "elasticloadbalancing:DeregisterTargets"
            ],
            "Resource": "arn:aws:elasticloadbalancing:*:*:targetgroup/*/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:SetWebAcl",
                "elasticloadbalancing:ModifyListener",
                "elasticloadbalancing:AddListenerCertificates",
                "elasticloadbalancing:RemoveListenerCertificates",
                "elasticloadbalancing:ModifyRule"
            ],
            "Resource": "*"
        }
    ]
}
```
2. Create IAM Role **AmazonEKSLoadBalancerControllerRole** of Web Identity type with above created Policy, use trust-policy of Role as json written below
<br><br/>
Retrieve EKS cluster's OIDC provider ID using the command as written below
```
aws eks describe-cluster --name <EKS-Cluster-Name> --query "cluster.identity.oidc.issuer" --output text | cut -d '/' -f 5
```
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Federated": "arn:aws:iam::111122223333:oidc-provider/oidc.eks.<REGION>.amazonaws.com/id/EXAMPLED539D4633E53DE1B71EXAMPLE"
            },
            "Action": "sts:AssumeRoleWithWebIdentity",
            "Condition": {
                "StringEquals": {
                    "oidc.eks.<REGION>.amazonaws.com/id/EXAMPLED539D4633E53DE1B71EXAMPLE:aud": "sts.amazonaws.com",
                    "oidc.eks.<REGION>.amazonaws.com/id/EXAMPLED539D4633E53DE1B71EXAMPLE:sub": "system:serviceaccount:kube-system:aws-load-balancer-controller"
                }
            }
        }
    ]
}
```

![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/2fe3d1ca-135b-4728-97fc-4d0b14e9553d)
<br><br/>
**Edit the trust-relationship of the created policy as shown in the screenshot below.**
<br><br/>
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/bb29f91f-219f-4850-ad31-5adf5f10fa71)
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/d57a8150-44ae-4c84-83a1-7a03a9b5cce6)
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/2c256ebb-e41f-4123-889e-d0b2b451208a)
<br><br/>
3. create Service Account using yaml as written below
```
cat sa.yaml

apiVersion: v1
kind: ServiceAccount
metadata:
  labels:
    app.kubernetes.io/component: controller
    app.kubernetes.io/name: aws-load-balancer-controller
  name: aws-load-balancer-controller
  namespace: kube-system
  annotations:
    eks.amazonaws.com/role-arn: arn:aws:iam::111122223333:role/AmazonEKSLoadBalancerControllerRole    ### Provide ARN of above created IAM Role AmazonEKSLoadBalancerControllerRole 
```
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/ed03f2f0-a722-43e3-99ef-50b4a143e48c)
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/39680247-b379-47f8-ab99-a155c679821b)
<br><br/>
kubectl apply -f sa.yaml
<br><br/>
4. Install cert-manager
```
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.13.5/cert-manager.yaml
```
5. Install AWS Load Balancer Controller
```
curl -Lo v2_7_2_full.yaml https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.7.2/v2_7_2_full.yaml
```
**Open file v2_7_2_full.yaml and delete below mentioned lines**
```
apiVersion: v1
kind: ServiceAccount
metadata:
  labels:
    app.kubernetes.io/component: controller
    app.kubernetes.io/name: aws-load-balancer-controller
  name: aws-load-balancer-controller
  namespace: kube-system
---
```
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/2b286eff-fd5b-4e7e-bce7-38be5e4b26de)
<br><br/>
**Replace your-cluster-name in the Deployment spec section of the file with the name of your eks cluster.**
<br><br/>
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/cf082762-9620-4044-8994-ff12cf39548e)
```
kubectl apply -f v2_7_2_full.yaml
curl -Lo v2_7_2_ingclass.yaml https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.7.2/v2_7_2_ingclass.yaml
kubectl apply -f v2_7_2_ingclass.yaml
```
6. Verify Installation of aws load balancer controller with below command
```
kubectl get deployment -n kube-system aws-load-balancer-controller
```
<br><br/>
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/813a4463-e368-41b5-8fee-21efa86afb1b)

<br><br/>
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/c9c16c6f-1ce5-45a8-a4c4-a799de7096d7)
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/8f4d7ca2-3f80-48b5-8fbb-5af92bd24951)
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/3c10b969-cba1-4a5e-b793-3fa533a6d2f5)
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/4af78b7c-4938-47f0-a78c-49750606c139)
<br><br/>
Finally do the entry of DNS Name of ALB into Route53 Reccord Set as shown in screenshot below and create the URL and access the created URL.
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/9110bd30-b124-42ba-8904-ca76bc1dccc3)
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/85bafca7-0595-41a5-a301-3a006a052ac6)
![image](https://github.com/singhritesh85/EKS-ApplicationLoadBalancer-Ingress-Controller/assets/56765895/466919fa-682d-435b-970a-dafd61132cee)

<br><br/>
**Reference** = https://docs.aws.amazon.com/eks/latest/userguide/lbc-manifest.html
