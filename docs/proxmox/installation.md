# Clean installation

Set final hostnames and management addresses before cluster creation. Verify firmware,
virtualization support, time synchronization, repository configuration, storage layout,
updates, and host access before joining nodes.

## Pre-install record

- Physical label and private serial/MAC mapping.
- CPU, RAM, NIC, disk model, disk health, and firmware.
- Virtualization and boot settings.
- Final hostname, management address, gateway, and DNS bootstrap values.
- Installation image source and checksum.

## Per-node validation

1. Confirm the expected disk was selected and the old installation may be erased.
2. Install with the final hostname; renaming a cluster node later is avoidable risk.
3. Apply updates and verify the node reboots cleanly.
4. Verify time, name resolution, gateway reachability, and management TLS.
5. Confirm storage names, capacity, thin-pool state, and reserved free space.
6. Confirm CPU virtualization, IOMMU requirements, guest agent support, and sensors.
7. Configure management firewall access before creating application guests.

Record the installer and package versions actually tested rather than claiming every
future version is compatible.
