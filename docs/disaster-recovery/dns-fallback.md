# DNS behavior during a rack outage

Keep public client DNS independent of cluster-hosted resolvers. A full rack outage may
remove the private split namespace, filtering, and internal applications, but it should
not require a router change to restore ordinary Internet name resolution.

## Preparation

- Store router credentials independently of the rack.
- Record the private resolver addresses and split namespace privately.
- Record the router's rack-independent public DNS baseline.
- Test both resolver and route-router failure domains.
- Keep an offline recovery copy of the DNS and overlay-policy procedure.

## Outage procedure

1. Verify the gateway and ISP path are healthy and both local resolvers are unavailable.
2. Confirm a client still uses its normal public resolver and resolves public names.
3. Confirm the private split namespace fails closed rather than leaking to public DNS.
4. Verify no stale global nameserver or broad route remains in the private-overlay policy.
5. Record the outage impact without weakening management or inter-VLAN policy.

## Restoration

Restore and test both local resolvers directly, then test each exact-route advertiser
and single-failure case. Republish the restricted split namespace only after the pair
passes. Do not restore private DNS merely because a guest process started; verify real
UDP/TCP queries, rewrites, filtering, and client resolution.
