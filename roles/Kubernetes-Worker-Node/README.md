# Kubernetes worker node
This playbook install Kubernetes and configures the host to be a worker node in an existing cluster.  The join token from the master is needed for this playbooks defaults.

## Example 
Here is an example of the k8s-worker.yaml file to deploy this playbook.<br>
<pre>
---
- hosts: localhost
  gather_facts: True
  become: True
  roles:
    - role: common
      vars:
        host_name: k8s-node1
        fqdn_hostname: k8s-node1.anet.internal
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

    - role: Kubernetes-Worker-Node
      vars:
        master_server: 192.168.4.10:6443
        cluster_token: s0mxuf.eo4km5jmmy7roypk
        discovery_token_ca_cert_hash: sha256:ada73b718f55a5e9106f9c69e820168333c9870c5e398d1fb13cbb4a23f29d70
</pre>
<br><br>
**ansible-playbook k8s-worker.yaml**
