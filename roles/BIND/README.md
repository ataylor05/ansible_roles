# BIND DNS server
something here

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
        selinux_state: enforcing
    - role: BIND
      vars:
        forward_zone_name: anet.local
        reverse_zone_name: "1.168.192"
        dns_sec: no
</pre>
<br><br>
**ansible-playbook main.yml**