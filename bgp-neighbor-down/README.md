# BGP Neighbor Down Investigation

## Incident Summary

A BGP session transitioned from Established state to Active state, preventing route exchange between peers.

## Impact Assessment

Potential impact included:

- Loss of route advertisements
- Service reachability issues
- Traffic forwarding disruption
- Redundant path unavailability

## Initial Investigation

Verify current BGP status:

```bash
show bgp summary
```

Expected:

```text
Neighbor        AS      State
10.10.10.1      65001   Established
```

Review recent changes:

- Network maintenance
- Route policy updates
- Firewall changes
- Interface modifications

## Technical Analysis

### Verify Reachability

```bash
ping 10.10.10.1
```

### Verify Route Path

```bash
traceroute 10.10.10.1
```

### Verify TCP Connectivity

```bash
nc -zv 10.10.10.1 179
```

### Verify Routing Table

```bash
ip route
```

### Review BGP Configuration

Verify:

- Local ASN
- Remote ASN
- Neighbor IP
- Route policies
- Source interface

### Review Logs

```bash
journalctl -u frr
```

## Root Cause Analysis

Potential causes:

- Network connectivity failure
- ASN mismatch
- Firewall blocking TCP/179
- Route policy issue
- Routing daemon issue

## Corrective Actions

- Restore connectivity
- Correct peer configuration
- Update route policies
- Restart routing services if required

## Verification

```bash
show bgp summary
```

Confirm:

- Neighbor state Established
- Routes received
- Routes advertised
- Service reachability restored

## Lessons Learned

- Verify reachability before protocol troubleshooting.
- Validate route advertisements after every change.
- Review route policies during investigation.
