# Kubernetes Master server for control plane
This playbook install a master Kubernetes server along with the flannel CNI network plugin.  After cluster initialization, the join token output will be saved to a file at /root/k8s-init.  Refer to this file for joining worker nodes.

## Example 
Here is an example of the k8s-master.yaml file to deploy this playbook.<br>
<pre>
---
- hosts: localhost
  gather_facts: True
  become: True
  roles:
    - role: common
      vars:
        host_name: k8s-master
        fqdn_hostname: k8s-master.anet.internal
        selinux_state: disabled
        root_pw: Passw@ord123!

    - role: NTP
      vars:
        ntp_network_access: 192.168.4.0/24

    - role: SSSD-Join-Domain
      vars:
        domain_name: anet.internal
        domain_join_user: administrator
        domain_join_pw: Passw@ord123!
        ad_dns_server: 192.168.4.2
        ad_linux_users_group_name: Linux_Admins
        ad_linux_admins_group_name: Linux_Users

    - role: Docker
      vars:
        user_added_to_docker_group: ansible

    - role: Kubernetes-Master-Control-Plane
      vars:
        k8s_admin_user: ansible
        k8s_init_output_file: /root/k8s-init
</pre>
<br><br>
**ansible-playbook k8s-master.yaml**
