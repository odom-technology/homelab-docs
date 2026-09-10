# Build a recoverable homelab

This project follows a small three-node Proxmox cluster behind a gateway, managed
switching, and Wi-Fi path that remains powered independently of the rack. Network zones
separate management, servers, public origins, household devices, sensors, and guests.
Server workloads are separated into guests, and the design is expected to be
reproducible from clean installations. A later fourth node may add compute and recovery
capacity only with independent quorum planning.

The first implementation stages are hardware inventory, final VLAN addressing and
firewall policy, Proxmox setup, redundant exact-route DNS, service deployment,
monitoring, off-host backups, and disaster-recovery testing.
