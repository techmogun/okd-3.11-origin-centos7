# okd-3.11-origin
okd 3.11 orgin

Step 1: Yum Update
```sh
yum -y update
```

Step 2: For password less login
```sh
ssh-keygen -t rsa
ssh-copy-id root@master.techmogun.local
```
Step 3: Yum install base packages
```sh
yum install -y wget git perl net-tools docker-1.13.1 bind-utils iptables-services bridge-utils openssl-devel bash-completion kexec-tools sos psacct python-cryptography python2-pip python-devel python-passlib java-1.8.0-openjdk-headless "@Development Tools"
yum -y install python-passlib httpd-tools; yum install -y epel-release; yum install -y ansible
```
Step 4: Git clone Openshift ansible
```sh
git clone https://github.com/openshift/openshift-ansible.git
cd openshift-ansible
git checkout release-3.11
```
Step 5: Download the inventory (Change the cluster hosname to your own domain & wilcard domain for application apps.master.192.168.10.5.xip.io to your name like apps.<yourdomain>.<yourhostip>.xip.io)
```sh
wget https://raw.githubusercontent.com/techmogun/okd-3.11-origin/master/inventory_wildcard_external
```
Step 6: Run the playbook for prerequisites. It should completed in all the stages

```sh
ansible-playbook -i inventory_wildcard_external playbooks/prerequisites.yml
```
Step 7: Deploying the cluster
```sh
ansible-playbook -i inventory_wildcard_external playbooks/deploy_cluster.yml
```
#After deployment of cluster : Change the password of user ocpadmin & add cluster admin role to ocpadmin user
```sh
htpasswd -b /etc/origin/master/htpasswd ocpadmin <password>
oc adm policy add-cluster-role-to-user cluster-admin ocpadmin
```
#login to openshift webconsole in your browser
https://master.techmogun.local:8443
