# QEMU-Cloud-Security-Research
Research paper and presentation on defending against VM escape through host-side monitoring of the QEMU process.


# Operational Detection of Guest-to-Host Compromise via QEMU Process Telemetry

**Course:** MS Cybersecurity, NYU Tandon School of Engineering
**Author:** Joshua Buckwald
**Date:** April 2026

## Overview

This research investigates the operational detection of guest-to-host compromise (VM escape) in QEMU-based virtualized environments using host-level process telemetry.

VM escape — where an attacker breaks out of a virtual machine to gain control of the underlying host — is one of the most consequential attacks in cloud and multi-tenant infrastructure. Existing detection methods like Virtual Machine Introspection (VMI) provide strong isolation from attacker manipulation but introduce a "semantic gap": reconstructing meaningful OS behavior from raw memory state increases analytical complexity and delays detection.

This project explores an alternative. Because the QEMU process is the first host-side component any escaping attacker must interact with, monitoring it directly using `auditd` can surface anomalous behavior — unexpected shell execution, access to sensitive host resources — at the moment of compromise rather than after post-exploitation activity has begun.

## Key Findings

- **Near real-time detection:** QEMU process telemetry flagged anomalous activity immediately after payload execution, at the **Exploitation phase** of the Cyber Kill Chain.
- **Earlier than VMI:** Traditional VMI-based approaches detect activity at the **Actions on Objectives phase**, after the attacker has achieved meaningful access.
- **Lightweight and practical:** No semantic reconstruction of guest memory state required. The signals are directly observable host-side via `auditd`.

## Environment

- **Host OS:** Linux (KVM hypervisor)
- **Guest:** QEMU-based virtual machine
- **Monitoring tool:** `auditd` (Linux Audit Daemon)
- **Methodology:** Controlled simulation of post-exploitation behavior via QEMU process injection using a debugger; no specific CVE exploited

## Repository Contents

| File | Description |
|------|-------------|
| [Research Paper (PDF)](./Operational_Detection_of_Guest_to_Host_Compromise_via_QEMU_Process_Telemetry.pdf) | Full academic paper with methodology, results, and references |
| [Presentation Slides (PDF)](./Operational-Detection-of-Guest-to-Host-Compromise-via-QEMU-Process-Telemetry.pdf) | Slide deck from the April 2026 course presentation |
| [Presentation Video](https://youtu.be/zfGqwWraH0c) | Recorded walkthrough of the research and findings |

## References

1. P. Mishra, E. S. Pilli, V. Varadharajan, and U. Tupakula, "Intrusion detection techniques in cloud environment: A survey," *Journal of Network and Computer Applications*, vol. 77, pp. 18–47, 2017.
2. T. Garfinkel and M. Rosenblum, "A virtual machine introspection based architecture for intrusion detection," in *Proceedings of the Network and Distributed Systems Security Symposium (NDSS)*, 2003.
3. K. Zhang, J. Ma, and C. Li, "Using KVM events to detect VM memory-sharing lateral movement attacks in a virtualized environment," in *2024 IEEE International Symposium on Parallel and Distributed Processing with Applications (ISPA)*, 2024.