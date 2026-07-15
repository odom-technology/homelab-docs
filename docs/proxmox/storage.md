# Storage on small cluster nodes

Three small nodes with one SSD each should begin with simple local storage. LVM-thin
provides efficient guest allocation without implying redundancy.

## Capacity policy

- Reserve host and thin-pool headroom rather than allocating the advertised disk size.
- Set explicit limits for recordings, models, metrics, logs, caches, and images.
- Monitor thin-pool data and metadata separately.
- Treat snapshots as short-lived maintenance tools, not backups.
- Send backups to storage outside the protected node.
- Test restoration before deleting the original guest or data.

## Workloads that grow unexpectedly

- Camera recordings and event clips.
- AI model downloads and conversation data.
- Metrics, logs, and dashboard databases.
- CI workspaces, images, caches, and artifacts.
- Home-automation history.

A future NAS may provide backup and bulk data, but it introduces its own availability,
permissions, network, filesystem, encryption, and off-site-copy decisions.
