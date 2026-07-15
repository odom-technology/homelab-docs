# Three-node router-preserving reference design

```text
Internet
   |
Existing modem
   |
Existing home router: gateway, DHCP, Wi-Fi
   |
Managed access switch
   +-- Proxmox node 1: network core
   +-- Proxmox node 2: trusted home services
   +-- Proxmox node 3: applications and compute
```

## Why preserve the router?

The home Internet connection, Wi-Fi, and default gateway continue operating when every
server is stopped. This is a useful boundary when the homelab is an optional service
platform rather than the household's required router.

The tradeoff is reduced segmentation. A VLAN-capable access switch cannot provide
routed VLANs by itself. Workload separation initially relies on virtual guests, resource
limits, and firewalls; it does not isolate wireless cameras or household clients from
one another.

## Node roles

| Node | Primary responsibility | Example guests |
| --- | --- | --- |
| 1 | Quiet network core | Primary DNS, optional remote-access router |
| 2 | Trusted home systems | Secondary DNS, home automation, MQTT, camera processing |
| 3 | Applications/compute | Monitoring, private apps, public origin, CI, limited AI |

Roles describe default placement, not permanent coupling. Stable physical names should
not encode the current workload so guests can move during future redesigns.

## Availability boundaries

- Three cluster votes tolerate one unavailable node for cluster configuration.
- Two DNS guests tolerate one DNS-host failure.
- Local SSDs do not tolerate node or disk loss without backup.
- A cluster is not application high availability unless storage, guest restart, and
  application recovery have each been designed and tested.
- A rack outage preserves the router but may require temporary public DNS.

## Exposure boundaries

- Management and internal sites use private remote access.
- Public applications live in a separate guest and use outbound tunnel/proxy ingress.
- The router has no application port forwards.
- DNS is the only service intentionally advertised to ordinary home clients.
