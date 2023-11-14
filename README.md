# Pihole + Bind9 + Unbound

This is my raspberry-pi homelab setup. This setup uses Pihole for adblocking and Bind9 as upstream *split-horizon* with Unbound as recursive resolver for domains outside of the homelab. It uses the *ipvlan* network driver to add the containers directly to the homelab network.


## Usage
1. Copy the .env.example to .env and make sure you fill in *all* the variables according to your own environment.
2. Run the bootstrap.sh script

When running the bootstrap script it will do the following based on the .env file variables:
- Create basic Bind9 `named.conf` file and `.zone` file. 
- Create `unbound.conf` file. 
- Create script for bringing up virtual interface and activate as systemd service.
- Start containers with `docker-compose up -d`


Congratulations! 
You should now be all set with an awesome homelab dns system.

##### Environment variables:
| Variable     |Example value       | Desc                                                         |
|--------------|--------------------|--------------------------------------------------------------|
| WEBPASSWORD  | password           | Pihole admin password                                        |
| TZ           | Europe/Oslo        | Your timezone                                                |
| ROUTER_IP    | 192.168.0.1        | Your homelab's router/gateway ip                             |
| DHCP_START   | 192.168.0.8        | Start of range DHCP                                          |
| DHCP_END     | 192.168.0.100      | End of range DHCP                                            |
| PIHOLE_IP    | 192.168.0.5        | Ip to assign pihole                                          |
| BIND9_IP     | 192.168.0.6        | Ip to assign bind9                                           |
| UNBOUND_IP   | 192.168.0.7        | Ip to assign unbound                                         |
| IP_RANGE     | 192.168.0.4/30     | Range of ip's for the container network                      |
| SUBNET       | 192.168.0.0/24     | Your homelab's subnet                                        |
| RESERVED_IP  | 192.168.0.4        | Ip to reserve for container - host communication             |
| DHCP_ACTIVE  | false              | Whether to activate DHCP                                     |
| DOMAIN       | lab.home.arpa      | Your homelab's domain                                        |
| PARENT_IFACE | eth0               | Host interface to use for the container network              |
| VIRTUAL_IFACE| lab-dns            | Virtual interface name for container host communication      |
