# Sambda Active Directory primary domain controller
This playbook provisions a Samaba Active Directory domain controller.  BIND is used on the local domain controller(s) instead of the built-in Samba DNS.  Also Samaba is complied from source instead of using a prebuilt binary.  This was done for the inclusion of the samaba-tool program which provisions Active Directory.

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
        fqdn_hostname: ns1.anet.local
        selinux_state: disabled
        
    - role: BIND
      vars:
        forward_zone_name: anet.local
        reverse_zone_name: "1.168.192"
        dns_sec: no

    - role: Samba-PDC
      vars:
        domain_name: ANET
        realm: ANET.local
        administrator_password: Passw@ord123!
</pre>
<br><br>
**ansible-playbook main.yml**