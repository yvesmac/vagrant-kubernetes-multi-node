# <img src="https://github.com/devicons/devicon/blob/master/icons/vagrant/vagrant-original.svg" width="30" height="30" /> Vagrant Kubernetes Multi Node Local for Practice

My motivation to create this repository is make more easyer the learning of pure kubernetes implementation, focusing on IaC with Vagrant on local machine

This environment can be used to study for CKA/CKAD and CKS <a href="https://training.linuxfoundation.org/full-catalog/?_sft_product_type=certification&_sft_topic_area=cloud-containers" target="_blank">Linux Foundation Exams</a>

Kubernetes version: v1.23

### Hardware Recomendation
- 8GB minimum of memory. Ideal is 16GB+
- Processor with 4 cores+

# <img src="https://github.com/devicons/devicon/blob/master/icons/vagrant/vagrant-original.svg" width="30" height="30" /> <img src="https://github.com/devicons/devicon/blob/master/icons/kubernetes/kubernetes-plain.svg" width="30" height="30" />  Ingredients, a lot of them 👩‍🍳
You need install the following tools:
- Vagrant
- Virtual Box and Extension Pack
- VS Code
- Git
- Kubectl

# Usage/Examples

## To provision the cluster, execute the following commands.
```shell
git clone https://github.com/yvesmac/vagrant-kubernetes-multi-node.git
cd vagrant-kubernetes-multi-node
vagrant up
```

## To destroy the cluser
```shell
vagrant destroy -f
```

## Kubectl Configuration
Copy a file generated on configs folder to your user home
```shell
cp config ~/.kube/
```

## Make Kubernetes Dashboard accessible with kubectl proxy
```shell
kubectl proxy --address='0.0.0.0' --accept-hosts='^*$'
```

## Kubernetes Dashboard URL
```shell
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/overview?namespace=kubernetes-dashboard
```