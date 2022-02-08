# Setup Amazon EKS
* Amazon Elastic Kubernetes Service (Amazon EKS) is a managed service that you can use to run Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane or nodes. 
* Runs and scales the Kubernetes control plane across multiple AWS Availability Zones to ensure high availability.
* Automatically scales control plane instances based on load, detects and replaces unhealthy control plane instances, and it provides automated version updates and patching for them.
  
![Eks-cluster-image](https://docs.aws.amazon.com/eks/latest/userguide/images/what-is-eks.png) 


## pre-requisites:

* setup ec2 instance
___

> ## AWS EKS Setup

1.__Setup kubectl__

   * Download kubectl version 1.20
   * Grant execution permissions to kubectl executable.
   * Move kubectl onto /usr/local/bin.
   * Test that your kubectl installation was successful.

```
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
mv ./kubectl /usr/local/bin 
kubectl version --short --client
```

 2 . __Setup eksctl__
  
  * Download and extract the latest release.
  *  Move the extracted binary to /usr/local/bin.
  *  Test that your eksclt installation was successful
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp 

sudo mv /tmp/eksctl /usr/local/bin  #move tmp to bin 
eksctl version  # check version 
```

3 . __Create an IAM Role and attache it to EC2 instance__
```
Note: create IAM user with programmatic access if your bootstrap system is outside of AWS
```
IAM user should have access to

IAM

EC2

VPC

CloudFormation

4 . __Create your cluster and nodes__
```
eksctl create cluster --name cluster-name  \
--region region-name \
--node-type instance-type \
--nodes-min 2 \
--nodes-max 2 \ 
--zones <AZ-1>,<AZ-2>


example:
eksctl create cluster --name valaxy-cluster \
   --region ap-south-1 \
--node-type t2.small \
```
5 . __To delete the EKS clsuter__
```
  eksctl delete cluster <cluster-name> --region <region-name>
  ```
6 . __Validate your cluster using by creating by checking nodes and by creating a pod__

```
kubectl get node
kubectl run pod <image-name> --image=image-name
```



