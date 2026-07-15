# ODOM Homelab Docs

Public, sanitized documentation for planning, building, operating, securing, and
recovering a small three-node Proxmox homelab without making the home router dependent
on the server cluster.

The site is authored in Markdown and prepared for MkDocs. It documents transferable
methods, not the exact production inventory, addresses, credentials, domains, account
identifiers, camera locations, or private policy.

## Documentation map

- `getting-started/` — goals, prerequisites, constraints, and staged build plan.
- `architecture/` — physical, logical, trust, availability, and dependency views.
- `hardware/` — selection, rack, nodes, network equipment, power, and cooling.
- `proxmox/` — clean installation, three-node cluster, storage, guests, and maintenance.
- `network/` — router-preserving topology, DNS, remote access, and later segmentation.
- `services/` — design and recovery considerations for each service family.
- `security/` — threat modeling, secrets, updates, exposure, and verification.
- `operations/` — monitoring, maintenance, incident handling, and capacity.
- `backups/` — backup classes, retention, off-site planning, and restore tests.
- `disaster-recovery/` — rebuilding from clean installations.
- `contributing/` — writing, sanitization, diagrams, and validation.

See `LICENSE.md` for the split license covering written guidance and source code.
