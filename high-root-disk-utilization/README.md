# High Root Disk Utilization Investigation

## Incident Summary

Infrastructure monitoring reported root filesystem utilization above operational thresholds. Immediate investigation was required to prevent service impact and deployment failures.

## Impact Assessment

Potential impact included:

* Application instability
* Failed upgrades
* Inability to write logs
* Container runtime failures

## Initial Investigation

Verify filesystem usage:

```bash
df -h
```

Identify affected filesystem and utilization trend.

Review recent:

* Software installations
* Log growth
* Container deployments

## Technical Analysis

### Identify Major Consumers

```bash
du -xh / --max-depth=2 2>/dev/null | sort -hr | head
```

### Identify Large Files

```bash
find / -type f -size +500M 2>/dev/null
```

### Review Journal Growth

```bash
journalctl --disk-usage
```

### Review Container Runtime Usage

```bash
crictl images
```

### Review Core Dumps

```bash
find /var -name "core*" 2>/dev/null
```

### Review Temporary Files

```bash
du -sh /tmp/* 2>/dev/null
```

## Root Cause Analysis

Investigation identified excessive log accumulation and unused container images consuming the majority of root filesystem capacity.

## Corrective Actions

* Remove obsolete logs
* Rotate journal logs
* Remove unused images
* Clean temporary files
* Archive historical data

## Verification

```bash
df -h
```

Confirm filesystem utilization returned below operational threshold.

## Lessons Learned

* Implement retention policies.
* Monitor filesystem growth trends.
* Review image accumulation during maintenance windows.
