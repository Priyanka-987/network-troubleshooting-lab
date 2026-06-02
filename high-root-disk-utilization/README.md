# High Root Disk Utilization Investigation

## Incident Summary

Infrastructure monitoring reported excessive root filesystem utilization exceeding operational thresholds.

## Impact Assessment

Potential impact included:

- Service degradation
- Failed deployments
- Log generation issues
- Application instability

## Initial Investigation

Check filesystem usage:

```bash
df -h
```

Identify affected mount points.

## Technical Analysis

### Identify Large Directories

```bash
du -xh / --max-depth=2
```

### Identify Large Files

```bash
find / -type f -size +500M
```

### Review Journal Usage

```bash
journalctl --disk-usage
```

### Review Container Images

```bash
crictl images
```

### Review Temporary Files

```bash
du -sh /tmp/*
```

## Root Cause Analysis

Potential causes:

- Log accumulation
- Core dumps
- Temporary files
- Container image buildup
- Application-generated data

## Corrective Actions

- Remove unnecessary files
- Rotate logs
- Remove unused images
- Archive historical data

## Verification

```bash
df -h
```

Confirm utilization is within acceptable limits.

## Lessons Learned

- Monitor disk growth trends.
- Implement retention policies.
- Review storage utilization regularly.
