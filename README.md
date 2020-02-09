# my_helm_charts

<!-- TOC -->

- [my_helm_charts](#myhelmcharts)
- [About](#about)
  - [Contributing](#contributing)
  - [Developers](#developers)
  - [License](#license)
- [Prerequisites](#prerequisites)
  - [Configure Access Account AWS](#configure-access-account-aws)
  - [AWS Regions and Availability Zones](#aws-regions-and-availability-zones)
  - [Install Docker-CE](#install-docker-ce)
  - [Install Kops](#install-kops)
  - [Install Terraform 0.11](#install-terraform-011)
  - [Install Terraform 0.12](#install-terraform-012)
  - [Install Kubectl](#install-kubectl)
- [Management Kubernetes Cluster](#management-kubernetes-cluster)

<!-- TOC -->

# About

My Helm Charts for Kubernetes.

## Contributing

1. Install: git, kubernetes, aws-cli, helm, helmfile, kustomize, gcloud,
2. Clone the repository to your machine through the command: `git clone https://github.com/aeciopires/my_helm_charts.git`
3. Go to the project folder: `cd my_helm_charts`
4. Create a branch using the pattern: `git checkout -b US-${DEV_NAME}`. Example: *git checkout -b US-AECIO*
5. Develop the task
6. Execute the code in 'development' and 'test' environments
7. Do commit and push files to repository remote with command `git push --set-upstream origin US-${DEV_NAME}`. Example: *git push --set-upstream origin US-AECIO*
8. Create Pull Request (PR) to the `master` branch, using the notations patterns of the development process
9. Update the content with the suggestions of the reviewer (if necessary)

**WARNING:** Before start to contribute, run the command: `git pull origin master` to fetch the newest content of the main branch and avoid conflicts that can make you waste time.

## Developers

developer: Aécio dos Santos Pires<br>
mail: http://blog.aeciopires.com/contato

## License

GPL-3.0 2020 Aécio dos Santos Pires

# Prerequisites

## Configure Access Account AWS


You will need to create an Amazon AWS account. Create a 'Free Tier' account at Amazon https://aws.amazon.com/ follow the instructions on the pages: https://docs.aws.amazon.com/chime/latest/ag/aws-account.html and https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier-limits.html. When creating the account you will need to register a credit card, but since you will create instances using the features offered by the 'Free Tier' plan, nothing will be charged if you do not exceed the limit for the use of the features and time offered and described in the previous link.

After creating the account in AWS, access the Amazon CLI interface at: https://aws.amazon.com/cli/

Click on the username (upper right corner) and choose the "Security Credentials" option. Then click on the "Access Key and Secret Access Key" option and click the "New Access Key" button to create and view the ID and Secret of the key, as shown below (https://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html). The Access Key and Secret Key shown below are for illustration only. They are invalid and you need to exchange for the actual data generated for your account.

```bash
Access Key ID: YOUR_ACCESS_KEY_HERE
Secret Access Key: YOUR_SECRET_ACCESS_KEY_HERE
```
    
Create the directory below.

```bash
mkdir -p /home/USERNAME/.aws/
touch /home/USERNAME/.aws/credentials
```
    
Access `/home/USERNAME/.aws/credentials` file and add the following content. The Access Key and Secret Key shown below are for illustration only. They are invalid and you need to exchange for the actual data generated for your account.

```bash
[default]
aws_access_key_id = YOUR_ACCESS_KEY_HERE
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY_HERE
```

Install awscli package

CentOS:

```bash
sudo yum -y install awscli
```

Debian/Ubuntu:

```bash
sudo apt-get -y install awscli
```


## AWS Regions and Availability Zones

List of regions and availability zones in AWS.

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html

## Install Docker-CE

Follow instructions of page for install Docker-CE

* Ubuntu: https://docs.docker.com/install/linux/docker-ce/ubuntu/
* Debian: https://docs.docker.com/install/linux/docker-ce/debian/
* CentOS: https://docs.docker.com/install/linux/docker-ce/centos/


## Install Kops

Simple shell function for kops installation in Linux 64 bits.

Kubernetes documentation:

https://kubernetes.io/docs/getting-started-guides/kops/ 

Copy and paste this code:

```bash
sudo su

function install_kops {
if [ -z $(which kops) ]; then
    curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
    
    chmod +x kops-linux-amd64
    mv kops-linux-amd64 /usr/local/bin/kops
else
    echo "kops is most likely installed"
fi
}
 
install_kops

which kops

kops version

exit
```

---

Credits: Juan Pablo Perez - https://www.linkedin.com/in/juanpabloperezpeelmicro/ 

https://github.com/peelmicro/learn-devops-the-complete-kubernetes-course

---

## Install Terraform 0.11

Simple shell function for Terraform installation version 0.11 in Linux 64 bits.

Terraform documentation:

https://www.terraform.io/docs/index.html

Copy and paste this code:

```bash
sudo su
 
TERRAFORM_ZIP_FILE=terraform_0.11.14_linux_amd64.zip
TERRAFORM=https://releases.hashicorp.com/terraform/0.11.14
TERRAFORM_BIN=terraform11
 
function install_terraform11 {
if [ -z $(which $TERRAFORM_BIN) ]; then
    wget ${TERRAFORM}/${TERRAFORM_ZIP_FILE}
    unzip ${TERRAFORM_ZIP_FILE}
    sudo mv terraform /usr/local/bin/${TERRAFORM_BIN}
    rm -rf ${TERRAFORM_ZIP_FILE}
else
    echo "Terraform 11 is most likely installed"
fi
}
 
install_terraform11
 
which terraform11
 
terraform11 version
 
exit
```

---

Credits: Juan Pablo Perez - https://www.linkedin.com/in/juanpabloperezpeelmicro/ 

https://github.com/peelmicro/learn-devops-the-complete-kubernetes-course

---

## Install Terraform 0.12

Simple shell function for Terraform installation version 0.12 in Linux 64 bits.

Terraform documentation:

https://www.terraform.io/docs/index.html

Copy and paste this code:

```bash
sudo su
 
TERRAFORM_ZIP_FILE=terraform_0.12.20_linux_amd64.zip
TERRAFORM=https://releases.hashicorp.com/terraform/0.12.20
TERRAFORM_BIN=terraform12
 
function install_terraform12 {
if [ -z $(which $TERRAFORM_BIN) ]; then
    wget ${TERRAFORM}/${TERRAFORM_ZIP_FILE}
    unzip ${TERRAFORM_ZIP_FILE}
    sudo mv terraform /usr/local/bin/${TERRAFORM_BIN}
    ln -sfn /usr/local/bin/${TERRAFORM_BIN} /usr/local/bin/terraform
    rm -rf ${TERRAFORM_ZIP_FILE}
else
    echo "Terraform 12 is most likely installed"
fi
}
 
install_terraform12
 
which terraform12
 
terraform12 version
 
exit
```

---

Credits: Juan Pablo Perez - https://www.linkedin.com/in/juanpabloperezpeelmicro/ 

https://github.com/peelmicro/learn-devops-the-complete-kubernetes-course

---

## Install Kubectl

Simple shell function for Kubectl installation in Linux 64 bits

Kubectl documentation:

https://kubernetes.io/docs/reference/kubectl/overview/

Copy and paste this code:

```bash
sudo su
 
KUBECTL_BIN=kubectl
 
function install_kubectl {
if [ -z $(which $KUBECTL_BIN) ]; then
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/$KUBECTL_BIN
    chmod +x ${KUBECTL_BIN}
    sudo mv ${KUBECTL_BIN} /usr/local/bin/${KUBECTL_BIN}
else
    echo "Kubectl is most likely installed"
fi
}
 
install_kubectl
 
which kubectl
 
kubectl version
 
exit
```

---

Credits: Juan Pablo Perez - https://www.linkedin.com/in/juanpabloperezpeelmicro/ 

https://github.com/peelmicro/learn-devops-the-complete-kubernetes-course

---

# Management Kubernetes Cluster

How to start Kubernetes cluster by using Kops and Terraform

First create a `zone DNS private` in Router53 service of AWS with name `devopsinuse.com` or other domain name in region `us-east-2` (Ohio).

Second create a bucket S3 public with name `aecio.devopsinuse.com` or other domain name.

```bash
SSH_KEYS=~/.ssh/udemy_devopsinuse
 
if [ ! -f "$SSH_KEYS" ]
then
    echo -e "\nCreating SSH keys ..."
    ssh-keygen -t rsa -C "udemy.course" -N '' -f ~/.ssh/udemy_devopsinuse
else
    echo -e "\nSSH keys are already in place!"
fi
 
echo -e "\nCreating kubernetes cluster ...\n"

cd ~/udemy

kops create cluster \
 --name=aecio.devopsinuse.com \
 --state=s3://aecio.devopsinuse.com \
 --authorization RBAC \
 --zones=us-east-2a \
 --node-count=2 \
 --node-size=t2.micro \
 --master-size=t2.micro \
 --master-count=1 \
 --dns private \
 --out=terraform_code \
 --target=terraform \
 --ssh-public-key=~/.ssh/udemy_devopsinuse.pub

cd ~/udemy/terraform_code

terraform init
terraform validate
terraform plan
terraform apply
terraform show
```

Get the public IP of instace `master.aecio.devopsinuse.com` and create a entry in `/etc/hosts` file for public IP with name `api.aecio.devopsinuse.com` and execute the commands to validate cluster and list nodes.

```bash
kops validate cluster --state=s3://aecio.devopsinuse.com

kubectl get nodes --show-labels

ssh -i ~/.ssh/udemy_devopsinuse admin@api.aecio.devopsinuse.com

```

Delete cluster:

```bash
cd ~/udemy/terraform_code

terraform destroy --auto-approve

kops delete cluster \
 --name=aecio.devopsinuse.com \
 --state=s3://aecio.devopsinuse.com \
 --yes
```

Update cluster:

```bash
kops update cluster \
 --name=aecio.devopsinuse.com \
 --state=s3://aecio.devopsinuse.com \
 --out=terraform_code --target=terraform \
 --ssh-public-key=~/.ssh/udemy_devopsinuse.pub
```

---

Credits: Juan Pablo Perez - https://www.linkedin.com/in/juanpabloperezpeelmicro/ 

https://github.com/peelmicro/learn-devops-the-complete-kubernetes-course

---

