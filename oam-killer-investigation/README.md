# OAM Application Restart Investigation

## Incident Summary

An operational alarm indicated repeated application restarts within a Kubernetes-managed workload. The issue affected management-plane functionality and required investigation to determine whether the restart was caused by application failure, infrastructure resource constraints, or platform configuration issues.

## Impact Assessment

Potential impact included:

* Management service instability
* Increased application restart count
* Operational alarms
* Degraded platform observability

## Initial Investigation

Verify workload status:

```bash
kubectl get pods -A | grep -i oam
```

Review restart count:

```bash
kubectl get pods -A -o wide
```

Determine:

* Single pod affected
* Multiple replicas affected
* Node-specific issue
* Cluster-wide issue

Review recent:

* Deployments
* Upgrades
* Configuration changes

## Technical Analysis

### Review Pod Events

```bash
kubectl describe pod <pod-name>
```

Look for:

* OOMKilled
* FailedMount
* Probe failures
* Container exits

### Review Previous Container Logs

```bash
kubectl logs <pod-name> --previous
```

Correlate application failure timestamp.

### Review Resource Utilization

```bash
kubectl top pod <pod-name>
kubectl top node
```

Verify:

* Memory consumption
* CPU utilization
* Node pressure conditions

### Verify Resource Configuration

```bash
kubectl describe deployment <deployment-name>
```

Review:

* Requests
* Limits
* JVM heap settings (if applicable)

## Root Cause Analysis

Investigation confirmed the application was terminated by Kubernetes due to memory exhaustion.

Container events showed:

```text
Reason: OOMKilled
```

Memory consumption exceeded configured limits resulting in forced container termination and restart.

## Corrective Actions

* Increase memory limits
* Review application memory usage
* Adjust resource requests
* Restart workload

## Verification

Confirm:

```bash
kubectl get pods
```

Verify:

* Restart count stable
* No OOMKilled events
* Alarm cleared
* Application functionality restored

## Lessons Learned

* Review memory sizing during onboarding.
* Monitor memory trends before limits are reached.
* Correlate restart events with resource consumption.

```
```
