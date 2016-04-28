# playbook-bcec
playbooks for bcec deploying openstack servers

-互信（一般运维帮忙做好）：
1.add all nodes(ip) in manage-nodes.txt;
2.gen-sshkey in ansible server:
  #ssh-keygen(press enter to continue)
3.copy ssh id to nodes:
  #for ip in `cat manage-nodes.txt`; do echo $ip; ssh-copy-id -i root@$ip;
ansible all -m copy -a "src=/root/.ssh/id_rsa.pub dest=/root" -k
ansible all -m shell -a "cat /root/id_rsa.pub >> /root/.ssh/authorized_keys"
ansible all -m shell -a "rm -f /root/id_rsa.pub"
-编辑/etc/ansible/hosts，建立如下分组：
 [bcec_all]
 bcec_ntp
 bcec_ctl
 bcec_cpt
 bcec_vip
 [bcec_ntp]
 ntp-ip-0
 ntp-ip-1
 [bcec_ctl]
 ctl-ip-0
 ctl-ip-1
 ctl-ip-2
 [bcec_cpt]
 cpt-ip-0
 cpt-ip-1
 cpt-ip-2
 cpt-ip-3
 cpt-ip-4
 [bcec_vip]
 vip-ip-0
 vip-ip-1
 [memcache_ip_addresses]
 10.24.216.0/24

-yum源配置（一般运维帮忙做好）：
-ntp配置：
 ansible-playbook playbook-ntp.yml
-iptables配置:
 ansible-playbook playbook-iptables.yml
-libvirt配置:
 ansible-playbook playbook-libvirt.yml
-systemd-journald配置:
 ansible-playbook playbook-journald.yml
-selinux配置:
 ansible-playbook playbook-selinux.yml
-sysctl配置:
 ansible-playbook playbook-sysctl.yml
-memcached:
 ansible-playbook playbook-memcached.yml
 
 
-执行task：
 执行所有task：
 ansible-playbook example.yml
 执行部分task：
 ansible-playbook example.yml --tags "configuration,packages"
 跳过某些task：
 ansible-playbook example.yml --skip-tags "configuration,packages"


