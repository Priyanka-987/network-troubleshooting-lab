# Connectivity Testing Methodology

## Incident Summary

This runbook provides a structured approach for isolating communication failures between infrastructure components, Kubernetes workloads, and external services.

## Objective

Identify the exact layer where communication failure occurs and reduce unnecessary troubleshooting effort.

## Investigation Workflow

### Layer 1 - Reachability Verification

Verify basic connectivity:

```bash
ping <destination-ip>
```

Determine:

* Reachable
* Packet loss
* Latency issues

### Layer 2 - Route Path Analysis

```bash
traceroute <destination-ip>
```

Identify:

* Routing loops
* Unexpected hops
* Path interruption

### Layer 3 - DNS Resolution

```bash
nslookup application.example.com
```

Verify:

* Correct IP resolution
* DNS propagation
* Multiple record consistency

### Layer 4 - Port Accessibility

```bash
nc -zv <destination-ip> 443
```

Determine:

* Port reachable
* Connection refused
* Timeout

### Layer 7 - Application Validation

```bash
curl -kv https://application.example.com
```

Review:

* HTTP response code
* TLS negotiation
* Application response

## Advanced Verification

### Verify Service Endpoints

```bash
kubectl get endpoints -A
```

### Verify Pod-to-Pod Communication

```bash
kubectl exec -it <pod-name> -- sh
```

```bash
curl http://<service-ip>
```

### Verify Network Policies

```bash
kubectl get networkpolicy -A
```

### Verify Routes

```bash
ip route
```

## Root Cause Analysis

Classify failure into:

* DNS issue
* Routing issue
* Firewall issue
* Network policy issue
* Service issue
* Application issue

## Corrective Actions

Apply fixes according to identified failure layer.

## Verification

Repeat all failed tests and confirm successful communication.

## Lessons Learned

* Follow a layer-by-layer methodology.
* Avoid assumptions.
* Verify application functionality after network recovery.

