# Operations checklists

## Weekly

- Review critical alerts and unresolved service degradation.
- Confirm both DNS resolvers answer independently.
- Review node, guest, disk, thin-pool, and temperature trends.
- Confirm backup jobs completed and capacity remains within policy.

## Monthly

- Review available hypervisor, guest, application, and firmware updates.
- Test one representative file or configuration restore.
- Review expiring credentials and certificates.
- Review public exposure, runner credentials, and failed authentication events.
- Check rack airflow, dust, fans, cabling, and power connections.

## Quarterly

- Restore a complete noncritical guest into an isolated location.
- Exercise single-node maintenance and verify cluster quorum.
- Test one-DNS failure and the full-rack DNS fallback documentation.
- Review service resource allocations and storage-retention limits.
- Reconcile private inventory with physical labels.
- Review threat models and accepted risks.

## Before every material change

Record scope, dependencies, backup/restore evidence, expected user impact, validation,
rollback, and the observation period after completion.
