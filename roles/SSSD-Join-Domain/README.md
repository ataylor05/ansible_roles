# Sambda Active Directory primary domain controller
This playbook adds a Linux host to an Active Directory domain and configures AD access control for the host.

## Example 
Here is an example of the main.yml file to deploy this playbook.<br>
<pre>
---
- hosts: localhost
  gather_facts: True
  become: True
  roles:
    - role: common
      vars:
        host_name: srv1
        fqdn_hostname: srv1.anet.internal
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
</pre>
<br><br>
**ansible-playbook main.yml**