# OAM Application Restart Investigation

## Incident Summary

Unexpected application restart events triggered operational alarms and service instability.

## Impact Assessment

Potential impact included:

- Management service degradation
- Increased restart counts
- Service instability
- Operational alerts

## Initial Investigation

Review pod status:

```bash
kubectl get pods
```

Review restart counts.

## Technical Analysis

### Describe Pod

```bash
kubectl describe pod <pod-name>
```

### Review Current Logs

```bash
kubectl logs <pod-name>
```

### Review Previous Logs

```bash
kubectl logs <pod-name> --previous
```

### Review Resource Utilization

```bash
kubectl top pod <pod-name>
```

### Review Events

```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

## Root Cause Analysis

Potential causes:

- OOMKilled event
- Resource exhaustion
- Application crash
- Configuration issue
- Dependency failure

## Corrective Actions

- Adjust resource limits
- Review application configuration
- Resolve dependency issues
- Restart workload

## Verification

Confirm:

- Restart count stable
- No new alarms generated
- Resource utilization normal

## Lessons Learned

- Monitor memory trends.
- Review restart patterns.
- Validate resource sizing.
