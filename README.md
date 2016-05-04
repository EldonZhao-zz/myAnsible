# playbook-bcec
playbooks for bcec deploying openstack servers

-互信（一般运维帮忙做好）：
	#互信的ansible做法：
	ansible all -m copy -a "src=/root/.ssh/id_rsa.pub dest=/root" -k
	ansible all -m shell -a "cat /root/id_rsa.pub >> /root/.ssh/authorized_keys"
	ansible all -m shell -a "rm -f /root/id_rsa.pub"

-编辑/etc/ansible/hosts，建立如下分组：
 详见hosts文件
   
-yum源配置（一般运维帮忙做好）：

-yum配置（ok）：
    ansible-playbook playbook-yum.yml
-ntp配置（ok）：
    ansible-playbook playbook-ntp.yml
-iptables配置(ok):
    ansible-playbook playbook-iptables.yml
-libvirt配置(ok):
    ansible-playbook playbook-libvirt.yml
-systemd-journald配置(ok):
    ansible-playbook playbook-journald.yml
-selinux配置(ok):
    ansible-playbook playbook-selinux.yml
-sysctl配置(ok):
    ansible-playbook playbook-sysctl.yml
-memcached(ok):
    ansible-playbook playbook-memcached.yml
-keepalived(no-test):
    ansible-playbook playbook-keepalived.yml
-haproxy(no-test):
    ansible-playbook playbook-haproxy.yml
-sql(drbd处理):
-rabbitmq():
-docker():
-openstack-util():
-keystone():
-glance():
-nova():
-horizon():
-cinder():
-ceilometer():
-portal():
-heat():
-senlin():
 
 
-执行task：
	执行所有task：
	ansible-playbook example.yml
	执行部分task：
	ansible-playbook example.yml --tags "configuration,packages"
	跳过某些task：
	ansible-playbook example.yml --skip-tags "configuration,packages"


