# RikHole

Pi-hole setup for my Synology NAS.

## Notes

For simplicity, this uses host networking. The `WEBPORT` is modified to `7780` to avoid conflicting with anything running in 80 (e.g. Nginx).

## Setup 

### Initial

1. Clone this repository.
1. `docker-compose up -d`.
1. Point router DHCP DNS to the IP of the NAS

### Fixing reverse lookups

Reverse lookups won't work because Pi-hole isn't the DHCP server (that's still the router).

We can forward these instead:

1. Get a shell: `sudo docker exec -i -t pihole /bin/bash`
1. Add the following file:

```
# cat >> /etc/dnsmasq.d/10-lan-domain.conf
server=/rik.local/192.168.1.1
server=/1.168.192.in-addr.arpa/192.168.1.1
server=/2.168.192.in-addr.apra/192.168.1.1
```

(substituting as appropriate).

