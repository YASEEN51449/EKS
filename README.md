Step 1: EC2 Setup

Launch an Ubuntu instance in your favourite region (eg. region ap-south-1).
SSH into the instance from your local machine.
sudo apt update 

******************************************Step 2: Install AWS CLI v2*****************************

	curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
	sudo apt install unzip
	unzip awscliv2.zip
	#which aws
	sudo ./aws/install -i /usr/local/aws-cli -b /usr/local/bin --update
	aws --version

*****************************************Step 3: IAM Configuration************************************

Create a user eks-user with Administrator Access.----Provides Sec Access key to create cluster----After Creating --->Create access key at CLI---download
create eks-role and provide these AmazonEC2ContainerRegistryFullAccess,AmazonEKSClusterPolicy,Iamfullaccess
Generate Security Credentials: Access Key and Secret Access Key.

*******************************************AWS CONFIGURATION************************************************
			aws configure
			aws s3 ls
----PASTE HERE ACCESS KEY & SECRET KEY---------

***************************************Step 4: Install kubectl**********************************************

	curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
	ls
	chmod +x ./kubectl [Changed to Executable Permission File]
	sudo mv ./kubectl /usr/local/bin
	kubectl version --short --client
	kubectl version

**************************************Step 5 : Install eksctl*******************************************

	curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
	sudo mv /tmp/eksctl /usr/local/bin
	eksctl version
      # eksctl help

**************************************Step 6: Setup EKS Cluster******************************************
                
	eksctl create cluster --name cluster --region ap-south-1 --node-type t2.micro --nodes-min 2 --nodes-max 2

						[or]

         eksctl create cluster --name cluster --region ap-south-1 --nodegroup-name worker --node-type t2.micro --nodes 3 --	 nodes-min 2 --nodes-max 2 --managed

   	 aws eks update-kubeconfig --region ap-south-1 --name cluster
	 kubectl get nodes
	 eksctl get clusters
 	 sudo yum install git -y
	 git clone https://github.com/nspacer/eks-basics.git
	 cd eks-basics/
	 cat nginx deployment.yaml
	 cat nginx-svc.yaml
	 kubectl apply -f ./nginx-svc.yaml
	 kubectl get service
	 kubectl apply -f ./nginx-deployment.yaml
	 kubectl get deployment
	 kubectl get pod
	 kubectl get node
	 kubectl get rs
	 curl loadbalancer dns name









