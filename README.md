# Network Troubleshooting Lab

This repository contains practical network and infrastructure troubleshooting scenarios based on operational incidents commonly encountered in cloud-native and telecommunications environments.

The objective of this repository is to demonstrate a structured troubleshooting methodology including impact assessment, technical investigation, root cause analysis, corrective actions, and service recovery validation.

## Scenarios

| Scenario | Description |
|-----------|-------------|
| BGP Neighbor Down | Investigation of routing peer failures and route exchange issues |
| Gateway Unavailable | Analysis of service accessibility and traffic forwarding problems |
| ECFE Configuration Synchronization | Investigation of configuration mismatch and synchronization failures |
| High Root Disk Utilization | Analysis of filesystem capacity and storage consumption issues |
| OAM Application Restart Investigation | Kubernetes application restart and resource analysis |
| Connectivity Testing Methodology | Structured approach for isolating communication failures |

## Skills Demonstrated

### Networking

- BGP Troubleshooting
- Route Validation
- Network Reachability Analysis
- Traffic Flow Verification
- Gateway Investigation
- Connectivity Testing

### Kubernetes

- Pod Investigation
- Service Troubleshooting
- Endpoint Verification
- Resource Analysis
- Event Analysis
- Log Analysis

### Linux Administration

- Filesystem Analysis
- Process Investigation
- Service Validation
- Resource Monitoring
- Log Management

### Operational Support

- Root Cause Analysis
- Incident Investigation
- Service Recovery
- Alarm Analysis
- Change Verification
- Troubleshooting Methodology

## Troubleshooting Framework

Each scenario follows a structured investigation process:

1. Incident Summary
2. Impact Assessment
3. Initial Investigation
4. Technical Analysis
5. Root Cause Analysis
6. Corrective Actions
7. Verification
8. Lessons Learned

## Investigation Methodology

```text
Alarm / Incident
       │
       ▼
Impact Assessment
       │
       ▼
Initial Investigation
       │
       ▼
Technical Analysis
       │
       ▼
Root Cause Analysis
       │
       ▼
Corrective Actions
       │
       ▼
Verification
       │
       ▼
Incident Closure
```

This methodology is used throughout the repository to ensure a consistent and structured troubleshooting approach.

## Repository Structure

```text
network-troubleshooting-lab/
│
├── README.md
│
├── bgp-neighbor-down/
│   └── README.md
│
├── gateway-unavailable/
│   └── README.md
│
├── ecfe-config-stale/
│   └── README.md
│
├── high-root-disk-utilization/
│   └── README.md
│
├── oam-killer-investigation/
│   └── README.md
│
└── connectivity-testing/
    └── README.md
```

## Key Investigation Areas

The repository focuses on practical troubleshooting techniques including:

- Network connectivity validation
- Routing analysis
- Configuration verification
- Resource utilization analysis
- Application health investigation
- Alarm correlation
- Service recovery validation

## Disclaimer

All examples are based on lab environments and personal learning exercises. No customer, production, confidential, or proprietary information is included in this repository.
