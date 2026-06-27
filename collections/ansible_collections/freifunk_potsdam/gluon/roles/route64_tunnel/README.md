# route64_tunnel role

Configure a [route64 IPv6 tunnel](https://route64.org/) to provide IPv6
connectivity and subnets.

## Requirements

Systemd (networkd), Debian based system.

## Role Variables

- `route64_tunnel_ifname`: device name to use, defaults: `route64wg0`
- `route64_tunnel_ifprio`: prefix for systemd networkd files, defaults: `40`
- `route64_tunnel_private_key`: private key of wireguard tunnel
- `route64_tunnel_public_key`: public key of wireguard tunnel
- `route64_tunnel_listen_port`: listen port to accept connections (optional)
- `route64_tunnel_allowed_ips`: list of allowed IPs (optional)
- `route64_tunnel_endpoint`: tunnel endpoint address:port
- `route64_tunnel_persistent_keepalive`: keep alive interval (optional) 
- `route64_tunnel_addresses`: list of IP addresses the tunnel binds to
- `route64_tunnel_prefixes`: list of prefixes routed via `route64_tunnel_remote_ipv6`
- `route64_tunnel_remote_ipv6`: remote IPv6 address for routing prefixes

## Dependencies

Currently, there are no dependencies to other roles.

## Example Playbook

```yaml
- hosts: gw1
  collections:
    - freifunk_potsdam.gluon
  roles:
    - route64_tunnel
  vars:
    route64_tunnel_ifname: route64tb1337
    route64_tunnel_private_key: ...
    route64_tunnel_public_key: ...
    route64_tunnel_endpoint: 1.2.3.4:1337
    route64_tunnel_persistent_keepalive: 15
    route64_tunnel_addresses:
      - "fdfd:d7b4:e621::2/64"
    route64_tunnel_remote_ipv6: "fdfd:d7b4:e621::1"
    route64_tunnel_prefixes:
      - "fdfd:d7b4:e621::/64"
      - "fda9:b8c2:5989:b17c::/56"
    route64_tunnel_allowed_ips:
      - "::/0"
```

## License

CC0-1.0

