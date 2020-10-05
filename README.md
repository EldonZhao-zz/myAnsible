# bcec-ansible

## 一、工具概述：
playbooks for deploying bcec openstack servers
基于ansible开发的环境部署工具，提升部署效率。

## 二、工具开发概况：
* 编辑/etc/ansible/hosts，建立如下分组：
    详见hosts文件
* ssh互信配置（一般运维帮忙做好）：
    > 互信的ansible做法是基于本地ssh做互信：
	> ansible all -m shell -a "cat /root/id_rsa.pub >> /root/.ssh/authorized_keys"
	> ansible all -m copy -a "src=/root/.ssh/ dest=/root"
* yum源配置（ok）：
    ansible-playbook playbook-yum.yml
* ntp配置（ok）：
    ansible-playbook playbook-ntp.yml
* iptables配置(ok):
    ansible-playbook playbook-iptables.yml
* libvirt配置(ok):
    ansible-playbook playbook-libvirt.yml
* systemd-journald配置(ok):
    ansible-playbook playbook-journald.yml
* selinux配置(ok):
    ansible-playbook playbook-selinux.yml
* sysctl配置(ok):
    ansible-playbook playbook-sysctl.yml
* memcached(ok):
    ansible-playbook playbook-memcached.yml
* keepalived(no-test):
    ansible-playbook playbook-keepalived.yml
* haproxy(no-test):
    ansible-playbook playbook-haproxy.yml
* sql(drbd处理):
* rabbitmq(no-test):
    ansible-playbook playbook-rabbitmq.yml
* docker(no-test):
    ansible-playbook playbook-deocker.yml
* openstack-util(no-test):
    ansible-playbook playbook-openstack-util.yml
* keystone():
* glance():
* nova(compute-ok,rabbitmq的配置写死为跟控制节点ip一致，需要优化。):
    ansible-playbook playbook-nova.yml
* horizon():
* cinder():
* ceilometer():
* portal():
* heat():
* senlin():
 
## 三、工具使用流程： 
* 本地安装ansible工具：
> sudo apt-get install ansible

* 执行task：

** 执行所有task：
> ansible-playbook example.yml

** 执行部分task：
> ansible-playbook example.yml --tags "configuration,packages"
** 跳过某些task：
> ansible-playbook example.yml --skip-tags "configuration,packages"
