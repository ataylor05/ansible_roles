# Sambda Active Directory primary domain controller
This playbook provisions a Samaba Active Directory domain controller.  Samaba is complied from source instead of using a prebuilt binary.  This was done for the inclusion of the samaba-tool program which provisions Active Directory.

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
        host_name: ad1
        fqdn_hostname: ad1.anet.internal
        selinux_state: disabled
        root_pw: Passw@ord123!

    - role: NTP
      vars:
        ntp_network_access: 192.168.4.0/24

    - role: Samba-PDC
      vars:
        samba_version: "4.12.6"
        domain_name: anet
        realm: anet.internal
        administrator_password: Passw@ord123!
        dns_backend: SAMBA_INTERNAL
</pre>
<br><br>
**ansible-playbook main.yml**