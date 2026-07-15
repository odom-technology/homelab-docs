# Staged build plan

Building in stages limits the number of unknowns introduced at once. Do not move to the
next stage until the current stage has documented verification and rollback.

## Stage 0: record and prepare

- Label physical nodes and record hardware identifiers privately.
- Confirm every installation disk may be erased.
- Record the router subnet, DHCP range, and an infrastructure address block.
- Prepare verified installation media and independent administrator credentials.
- Remove dependencies on any server that will be reinstalled.
- Define temporary DNS behavior during the rebuild.

## Stage 1: install the cluster

1. Install the first node with its final hostname and management address.
2. Update and validate storage, networking, time, and management access.
3. Create the named cluster.
4. Install and join the second and third nodes.
5. Verify votes, time synchronization, certificates, and node-to-node communication.

Do not deploy applications on hypervisor hosts.

## Stage 2: establish network services

- Create two small DNS guests on separate physical nodes.
- Configure and test each resolver independently.
- Monitor TCP and UDP resolution.
- Only then advertise both addresses through router DHCP.
- Test the full-rack manual DNS fallback.

## Stage 3: trusted home services

- Deploy MQTT if required by the home-automation and camera design.
- Deploy Home Assistant and verify backup restoration.
- Test camera streams and hardware acceleration before setting recording retention.
- Deploy Frigate with strict storage limits.

## Stage 4: visibility and backups

- Monitor DNS, cluster quorum, guests, disks, temperature, services, and backups.
- Establish a backup target outside each node.
- Define retention and encryption.
- Restore representative guests and data into an isolated location.

## Stage 5: applications and remote access

- Add internal applications behind private remote access.
- Design remote-access roles around service identities, not temporary IP addresses.
- Add a dedicated public-app guest and outbound ingress only when an application exists.
- Add CI runners with narrow deployment credentials.

## Stage 6: recovery exercise

Rebuild at least one noncritical guest from source and backup. Then rehearse node loss,
single-DNS loss, full-rack DNS fallback, and restoration of a critical data service.
