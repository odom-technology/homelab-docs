# Build a recoverable homelab

This project follows a small three-node Proxmox cluster connected to an existing home
router through a managed switch. The router remains responsible for Internet access,
Wi-Fi, DHCP, and the default gateway. Server workloads are separated into guests, and
the design is expected to be reproducible from clean installations.

The first implementation stages are hardware inventory, addressing, Proxmox setup,
redundant DNS, service deployment, monitoring, backups, and disaster-recovery testing.
