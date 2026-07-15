# Keep the existing router independent

In this design, the server cluster is connected to a LAN switch behind the existing
router. The router remains responsible for the ISP handoff, firewall/NAT, DHCP, Wi-Fi,
and the default gateway.

## Benefits

- Reinstalling or shutting down the cluster does not remove Wi-Fi or routing.
- Household devices keep the familiar gateway and wireless configuration.
- The homelab can be developed incrementally.
- A virtual-router mistake cannot directly strand the household.

## Limitations

- Consumer routers may have limited VLAN and firewall capabilities.
- Wireless IoT/cameras remain on router-provided networks unless the router supports a
  suitable guest or IoT isolation mode.
- Server guests on the flat LAN can reach other LAN devices unless host/guest firewalls
  restrict them.
- DNS filtering still depends on the cluster when clients are configured to use it.

## Safe initial changes

- Reserve addresses for hypervisors and infrastructure guests.
- Advertise two validated local DNS resolvers through LAN DHCP.
- Configure IPv6 DNS consistently or explicitly defer IPv6.
- Avoid router port forwards; use outbound public ingress when required.
- Export and protect the router configuration before material changes.
