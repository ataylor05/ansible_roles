# Chrony NTP server
something here

## Example 
Here is an example of the main.yml file to deploy this playbook.<br>
<pre>
- hosts: localhost
  gather_facts: True
  become: True
  roles:
    - role: common
      vars:
        fqdn_hostname: ns1.anet.local
        selinux_state: enforcing

    - role: NTP
      vars:
        ntp_network_access: 192.168.4.0/24
</pre>
<br><br>
**ansible-playbook main.yml**