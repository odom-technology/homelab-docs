# Three-node cluster

A three-node cluster retains quorum when one node is unavailable. It does not make
local disks redundant or move guests automatically. Document cluster creation, join
order, expected votes, safe shutdown, node replacement, and quorum-loss behavior.

## Join sequence

Create the cluster on the first fully validated node. Join the other two only after
their final hostnames, addresses, storage, updates, and time are correct. Joining a node
overwrites parts of its cluster configuration, so it should not contain important
guests beforehand.

## Acceptance checks

- All three nodes appear with one expected vote each.
- Node names and management addresses match the private inventory.
- Clocks remain synchronized.
- Management certificates and browser access work as intended.
- A controlled single-node shutdown leaves two-node quorum.
- Guests are configured with documented startup and shutdown ordering.
- Node removal and replacement procedures exist before hardware fails.

Do not lower expected votes as a routine fix for a failed node. Understand and document
the failure before changing quorum behavior.
