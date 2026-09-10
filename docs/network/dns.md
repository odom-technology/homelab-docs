# DNS and AdGuard Home

Run two resolvers on different physical nodes and reach them through two identical,
narrowly routed failure domains. Keep router DHCP and ordinary client public DNS on
rack-independent resolvers. Publish the local pair only for a restricted private split
namespace after UDP/TCP, rewrite, filtering, and failover tests pass.

## Independent resolvers

“Primary” and “secondary” are administrative labels. Clients may query either address,
so both instances must have equivalent policy and be able to resolve independently.
Do not make the second instance depend on the first for startup.

## Deployment acceptance

- Direct UDP and TCP queries succeed against both resolvers.
- Filtering and required local rewrites match.
- Resolver administration is not exposed to untrusted LAN or Internet clients.
- Query-log retention and backup treatment are intentional.
- IPv4 and IPv6 clients cannot silently bypass the intended policy.
- Both exact-route advertisers reach both local resolvers without exposing a whole
  server or management network.
- Private split DNS publishes both local addresses only after validation.
- An end-user lookup test detects failure beyond process-level health.
- With the entire rack off, public names still resolve and only the private namespace is
  unavailable.

Remote ad filtering is a separate design decision. Do not turn a private split-DNS
deployment into a global DNS dependency without repeating full-rack failure analysis.
