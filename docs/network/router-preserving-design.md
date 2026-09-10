# Keep the network core independent

In this design, the modem, gateway/firewall, primary switch, and Wi-Fi AP remain outside
the virtualized cluster and retain independent power. The cluster connects through a
rack switch only after the management and server VLANs are tested.

## Benefits

- Reinstalling or shutting down the cluster does not remove Wi-Fi or routing.
- Household devices keep routing, DHCP, Wi-Fi, and public DNS during rack maintenance.
- The homelab can be developed incrementally.
- A virtual-router failure cannot strand the household because no hypervisor is the
  gateway.

## Limitations

- The gateway, switches, and AP must all support the required VLAN tags and policy.
- Single-NIC hypervisors require carefully validated trunks and console recovery.
- Private names still disappear during a full rack outage.
- Entry-level managed switches rely heavily on physical port security when 802.1X is
  unavailable.

## Safe initial changes

- Reserve final management and server addresses before installing hypervisors.
- Establish default-deny inter-VLAN policy and a direct recovery port before adding
  compute.
- Keep public client DNS rack-independent; publish only a restricted private split
  namespace after both resolver and route-router failure tests pass.
- Configure IPv6 firewall and DNS consistently or explicitly keep IPv6 disabled.
- Avoid router port forwards; use outbound public ingress when required.
- Export and protect the router configuration before material changes.
