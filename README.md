# Ansible Role: NAT Router

Setup an Ubuntu host as a NAT router following these [instructions](https://help.ubuntu.com/community/Internet/ConnectionSharing#Ubuntu_Internet_Gateway_Method_.28iptables.29).

Tested on Ubuntu 16.04.

## Role Variables

The following variables can be used to customize the role:

    wan_interface: eth0

Name of external network interface.

    lan_interface: eth1

Name of internal network interface.

    lan_ip_range: 192.168.0.0/24

IP address range of the internal network.

    dhcp_range: 192.168.0.100,192.168.0.250

IP address range used by the internal DHCP server.

    fixed_leases: []

List of pairs of MAC address and IP address to allocate statically.

    port_forwards: []

List of port forwards.

## Example Playbook

```yaml

    - hosts: all
      become: yes
      roles:

        - role: nat-router
          wan_interface: enp4s0
          lan_interface: enp6s0
          lan_ip_range: 192.168.1.0/24
          dhcp_range: 192.168.1.100,192.168.1.200
          fixed_leases:
            - ["66-40-3B-5E-06-F0", "192.168.1.100"]
            - ["42-A8-CE-A1-BE-9D", "192.168.1.101"]
          port_forwards:
            - port: 8079
              protocol: tcp
              destination: 192.168.0.100:80
            - port: 8078
              protocol: tcp
              destination: 192.168.0.101:81
```

## License

MIT
