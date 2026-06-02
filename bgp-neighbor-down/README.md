# BGP Neighbor Down Investigation

## Incident Summary

A routing alarm indicated that a BGP session had transitioned from Established state to Active state, resulting in route exchange failure between peers.

## Impact Assessment

Potential impact included:

* Loss of route advertisements
* Traffic forwarding disruption
* Service reachability issues
* Redundant path unavailability

## Initial Investigation

Verify current BGP status:

```bash
show bgp summary
```

Example:

```text
Neighbor        AS      State
10.10.10.1      65001   Active
```

Expected state:

```text
Neighbor        AS      State
10.10.10.1      65001   Established
```

Determine whether the issue affects:

* Single neighbor
* Multiple neighbors
* Entire routing domain

## Technical Analysis

### Verify Layer 3 Reachability

```bash
ping 10.10.10.1
```

### Verify Routing Path

```bash
traceroute 10.10.10.1
```

### Verify TCP Connectivity

```bash
nc -zv 10.10.10.1 179
```

### Verify Local Routing Table

```bash
ip route
```

### Verify BGP Configuration

Review:

* Local ASN
* Remote ASN
* Neighbor IP
* Source interface
* Route policies

### Review Routing Daemon Logs

```bash
journalctl -u frr
```

or

```bash
kubectl logs <speaker-pod>
```

### Validate Route Advertisement

```bash
show bgp ipv4 unicast summary
show bgp ipv4 unicast neighbors
```

Verify:

* Advertised routes
* Received routes
* Prefix count
* Route filtering

## Root Cause Analysis

Potential root causes:

* Network connectivity loss
* Incorrect ASN configuration
* Neighbor configuration mismatch
* Firewall blocking TCP/179
* Route policy issue
* Routing daemon failure

## Corrective Actions

* Restore network connectivity
* Correct BGP peer configuration
* Update route policies
* Restart routing service if required
* Verify route exchange

## Verification

Confirm:

```bash
show bgp summary
```

Neighbor state:

```text
Established
```

Verify:

* Routes are received
* Routes are advertised
* Service reachability restored

## Lessons Learned

* Validate reachability before reviewing protocol behavior.
* Review route policies whenever advertisements are missing.
* Confirm both control-plane and data-plane functionality before incident closure.

