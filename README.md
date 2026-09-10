# ODOM Homelab Docs

Public, sanitized documentation for planning, building, operating, securing, and
recovering a small Proxmox homelab without making household routing, Wi-Fi, or public
DNS dependent on the server cluster.

The site is authored in Markdown and prepared for MkDocs. It documents transferable
methods, not the exact production inventory, addresses, credentials, domains, account
identifiers, camera locations, or private policy.

## Documentation map

- `getting-started/` — goals, prerequisites, constraints, and staged build plan.
- `architecture/` — physical, logical, trust, availability, and dependency views.
- `hardware/` — selection, rack, nodes, network equipment, power, and cooling.
- `proxmox/` — clean installation, three-node cluster, storage, guests, and maintenance.
- `network/` — rack-independent routing, segmented networks, split DNS, and remote access.
- `services/` — design and recovery considerations for each service family.
- `security/` — threat modeling, secrets, updates, exposure, and verification.
- `operations/` — monitoring, maintenance, incident handling, and capacity.
- `backups/` — backup classes, retention, off-site planning, and restore tests.
- `disaster-recovery/` — rebuilding from clean installations.
- `contributing/` — writing, sanitization, diagrams, and validation.

See `LICENSE.md` for the split license covering written guidance and source code.

## Reference design

The reference system uses three small Proxmox nodes, local SSDs, a rack-independent
gateway/switch/AP path, management and service VLANs, redundant AdGuard guests,
exact-route private access, and separate outbound-only public origins. A later fourth
node is reserved for compute, CI isolation, and recovery. Begin with the
[reference design](docs/architecture/reference-design.md) and
[staged build plan](docs/build-plan/index.md).
