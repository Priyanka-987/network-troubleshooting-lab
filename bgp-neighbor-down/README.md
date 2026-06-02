# BGP Neighbor Down Investigation

## Incident Summary

A routing alarm indicated that a BGP peer session transitioned from Established state to Active state, resulting in route exchange failure between neighboring systems.

## Impact Assessment

Potential impact included:

* Route withdrawal
* Traffic forwarding disruption
* Service reachability issues
* Reduced network redundancy

## Initial Investigation

Verify BGP session status:

```bash
show bgp summary
```

Example:

```text
Neighbor        State
10.10.10.1      Active
```

Expected:

```text
Neighbor        State
10.10.10.1      Established
```

Review recent:

* Network maintenance
* Configuration changes
* Route policy updates
* Infrastructure upgrades

Determine:

* Single peer affected
* Multiple peers affected
* Site-wide impact

## Technical Analysis

### Verify Reachability

```bash
ping 10.10.10.1
```

### Verify Route Path

```bash
traceroute 10.10.10.1
```

### Verify TCP Session

```bash
nc -zv 10.10.10.1 179
```

### Verify Routing Table

```bash
ip route
```

### Verify Neighbor Configuration

Review:

* Local ASN
* Remote ASN
* Neighbor address
* Update source
* Route policies

### Verify Routing Daemon Health

```bash
systemctl status frr
```

or

```bash
kubectl logs <speaker-pod>
```

### Verify Advertised Routes

```bash
show bgp ipv4 unicast neighbors
```

Review:

* Advertised prefixes
* Received prefixes
* Prefix filtering
* Route maps

### Verify Interface Status

```bash
ip addr
ip link
```

Review interface health and address assignment.

## Root Cause Analysis

Investigation identified a routing path failure between BGP peers causing TCP/179 communication failure.

Without an active TCP session, the BGP state machine remained in Active state and route exchange could not occur.

## Corrective Actions

* Restore Layer 3 connectivity.
* Verify neighbor configuration.
* Validate route policies.
* Restart routing process if required.
* Re-establish BGP session.

## Verification

Verify:

```bash
show bgp summary
```

Confirm:

```text
Established
```

Verify:

* Prefixes received
* Prefixes advertised
* Traffic forwarding restored
* Monitoring alarms cleared

## Lessons Learned

* Verify network reachability before investigating BGP protocol behavior.
* Review route advertisements after every routing change.
* Correlate routing alarms with transport-layer connectivity.
