# DNS fallback during a rack outage

Keeping the router independent preserves the Internet path, but clients configured to
use cluster-hosted DNS cannot resolve names while every server is off.

## Preparation

- Store router credentials independently of the rack.
- Record the normal local DNS addresses privately.
- Choose trusted temporary public resolvers before an outage.
- Know how clients receive a renewed DHCP lease.
- Keep a printed or offline copy of the router DNS procedure.

## Outage procedure

1. Verify the router and ISP path are healthy and both local resolvers are unavailable.
2. Record the current router DHCP DNS configuration.
3. Temporarily select public/automatic DNS.
4. Renew one test client's network configuration.
5. Verify resolution and record that filtering is bypassed.

## Restoration

Restore and test both local resolvers directly, return their addresses to router DHCP,
renew a test client, verify filtering, and record the incident. Do not restore local DNS
merely because a guest process started; verify real queries.
