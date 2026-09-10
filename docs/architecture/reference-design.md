# Three-node rack-independent segmented reference design

```text
Internet
   |
Modem -> gateway/firewall -> primary managed switch -> primary Wi-Fi AP
                                  |
                             rack switch
                       +----------+----------+
                       |          |          |
                 Proxmox 1  Proxmox 2  Proxmox 3
                 network     home/core    public
                   core       services   production
```

The modem, gateway, primary switch, and Wi-Fi AP remain powered independently of rack
compute. Reinstalling or shutting down every server therefore does not remove household
routing, Wi-Fi, DHCP, or public DNS.

## Network zones

The reference uses separate management, server, public/DMZ, IoT, sensor/camera, and
guest zones while retaining a trusted household network. Management and server zones
are established before Proxmox is built. Default inter-zone policy is deny; every
exception names the exact source, destination, protocol, and recovery purpose.

## Node roles

| Node | Primary responsibility | Example guests |
| --- | --- | --- |
| 1 | Quiet network core | Primary DNS, first exact-route router, internal status/ingress |
| 2 | Secondary core and trusted home systems | Secondary DNS/router, home automation, MQTT, observability, camera processing |
| 3 | Dedicated public production | Separate public origins and an initial ephemeral deployment runner |
| Future node 4 | Compute, CI isolation, and recovery | AI, sandbox, runner relocation, manual/warm public recovery |

The fourth node is not part of the initial three-vote cluster. Adding it requires an
independent quorum-device design; it is not a substitute for off-host backup.

## Availability boundaries

- Three cluster votes tolerate one unavailable node for cluster configuration.
- Two DNS guests and two identical exact-route advertisers tolerate one failure domain.
- A rack outage removes private names and rack services but leaves client-native public
  DNS, routing, and Wi-Fi available.
- Local SSDs do not tolerate node or disk loss without backup.
- A cluster is not application high availability unless storage, guest restart, and
  application recovery have each been designed and tested.

## Exposure boundaries

- Hypervisors use direct private-overlay identities; service routers advertise only
  approved individual destinations, never whole VLANs or a default route.
- Private DNS is published only as a restricted split namespace after both DNS and route
  failure domains pass.
- Each public application uses its own guest, outbound tunnel, credentials, firewall,
  health checks, and recovery procedure.
- Public origins, private services, and CI runners do not share an operating system.
- The gateway has no application port forwards, WAN management, UPnP, or DMZ host.
