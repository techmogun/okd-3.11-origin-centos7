# okd-3.11-origin
okd 3.11 orgin

Step 1:
```sh
ssh-keygen -t rsa
ssh-copy-id root@master
ssh-copy-id root@master.techmogun.local
```
```sh
yum install wget
yum install -y wget git perl net-tools docker-1.13.1 bind-utils iptables-services bridge-utils openssl-devel bash-completion kexec-tools sos psacct python-cryptography python2-pip python-devel python-passlib java-1.8.0-openjdk-headless "@Development Tools"
yum -y install python-passlib httpd-tools; yum install -y epel-release; yum install -y ansible
```

```sh
git clone https://github.com/openshift/openshift-ansible.git
cd openshift-ansible
git checkout release-3.11
wget 
```

```sh
ansible-playbook -i inventory_wildcard_external openshift-ansible/playbooks/prerequisites.yml
ansible-playbook -i inventory_wildcard_external openshift-ansible/playbooks/deploy_cluster.yml
```

#After deployment of cluster
```sh
htpasswd -b /etc/origin/master/htpasswd ocpadmin <password>
oc adm policy add-cluster-role-to-user cluster-admin ocpadmin
```
