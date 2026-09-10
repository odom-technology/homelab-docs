# Staged build plan

Building in stages limits the number of unknowns introduced at once. Do not move to the
next stage until the current stage has documented verification and rollback.

## Stage 0: record and prepare

- Label physical nodes and record hardware identifiers privately.
- Confirm every installation disk may be erased.
- Record the trusted subnet, DHCP range, final VLANs, static infrastructure addresses,
  and exact inter-zone permits.
- Prepare verified installation media and independent administrator credentials.
- Remove dependencies on any server that will be reinstalled.
- Keep client public DNS independent of the servers being rebuilt.

## Stage 1: establish the network foundation

- Create management and server VLANs without ordinary DHCP.
- Apply exact permits before default inter-zone denies.
- Configure switch trunks, rack access ports, AP management, and a direct recovery port.
- Verify trusted, IoT, sensor/camera, and guest connectivity is unchanged.
- Reboot the gateway, switches, and AP and verify saved state before attaching compute.

## Stage 2: install the cluster

1. Install the first node with its final hostname and management address.
2. Validate storage, time, direct private-overlay access, key-only SSH, and console
   recovery before creating the cluster.
3. Create the named cluster.
4. Install and join the second node, then document the two-vote operating constraint.
5. Add the third node only after its hardware and clean onboarding pass.
6. Verify votes, time synchronization, certificates, firewalls, and node-to-node traffic.

Do not deploy applications on hypervisor hosts.

## Stage 3: establish network services

- Create two small DNS guests on separate physical nodes.
- Create two service-router guests that advertise the same approved individual
  destinations, never whole VLANs or a default route.
- Configure and test each resolver independently.
- Monitor TCP and UDP resolution, filtering, local rewrites, and both route paths.
- Only then publish both addresses for a restricted private split namespace.
- Confirm a full-rack outage leaves public client DNS working without a router change.

## Stage 4: backups and trusted home services

- Establish encrypted off-host backup and complete a representative restore first.
- Deploy Home Assistant and MQTT with documented discovery and access policy.
- Test camera streams and hardware acceleration before setting recording retention.
- Deploy Frigate only with an external recording target or an explicitly bounded
  detection-only design.

## Stage 5: visibility

- Monitor DNS, cluster quorum, guests, disks, temperature, services, and backups.
- Keep observability on a different failure domain from public origins.
- Bound metrics and log retention and test authenticated alert delivery.

## Stage 6: public applications and CI

- Add internal applications behind purpose-specific private access.
- Place each public application in its own guest with its own outbound tunnel,
  credentials, firewall, health checks, and recovery procedure.
- Add an ephemeral CI runner with narrow deployment credentials; move it to a separate
  compute node when available.
- Keep public origins, private applications, CI, and AI out of shared operating systems.

## Stage 7: recovery exercise

Rebuild at least one noncritical guest from source and backup. Then rehearse node loss,
single-DNS and route-router loss, full-rack private-DNS loss, public-DNS continuity, and
restoration of a critical data service.
