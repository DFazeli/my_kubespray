# Deploy a Production Ready Kubernetes Cluster

## Quick Start

To deploy the cluster you can use :

#### Usage

```ShellSession
Important parameters that have been changed:
    Etcd is installed as systemD not docker.
    Container runtimes: containerd
    Metallb: True
    kube_network_plugin: calico
    kube_proxy_mode: ipvs
    kube_encrypt_secret_data: true
    nodelocaldns_ip: 192.68.8.10

    
Step1) # Install dependencies from ``requirements.txt`` on Ansible server.
          cd /opt
     sudo apt-get install python3-venv
     sudo python3 -m venv venv
     sudo apt install python3-pip
          pip3 install -U pip
          source venv/bin/activate
     sudo git clone https://github.com/DFazeli/my_kubespray.git
          cd my_kubespray
     sudo pip3 install -r requirements.txt
          ssh-keygen
          ssh-copy-id -i your_user@All_kubernetes_cluster_nodes_IP
     sudo vim /etc/resolv.conf
              185.51.200.2
              178.22.122.100

Step2) # Set inventory hosts 
     sudo declare -a IPS=(10.10.1.3 10.10.1.4 10.10.1.5)
     sudo CONFIG_FILE=inventory/newcluster/hosts.yaml python3 contrib/inventory_builder/inventory.py ${IPS[@]}
Or 
     sudo vim inventory/newcluster/inventory.ini

Step3) # If you want Review and change parameters under ``inventory/mycluster/group_vars``
      vim inventory/newcluster/group_vars/all/all.yml
      vim inventory/newcluster/group_vars/k8s_cluster/k8s_cluster.yml

Step4) # Run ansible playbook if your inventory file is [hosts.yaml] 
         ansible-playbook -i inventory/mycluster/hosts.yaml  -b --private-key=~/.ssh/id_rsa  cluster.yml
       OR  
         Run ansible playbook if your inventory file is [inventory.ini] (Do not forget to introduce your nodes)
           ansible-playbook -i inventory/mycluster/inventory.ini  -b --private-key=~/.ssh/id_rsa  cluster.yml
```
