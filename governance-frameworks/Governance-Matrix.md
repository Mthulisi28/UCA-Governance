# Unified Control Architecture (UCA) — Governance Control Matrix
**Classification:** Enterprise Compliance Framework Baseline

This document dictates the classification of preventative and detective controls implemented across all organizational units within the global landing zone.

| Control Domain | AWS Native Feature | Preventative | Detective | Continuous Assessment & Auditing Logic |
| :--- | :--- | :---: | :---: | :--- |
| **Identity & Access** | AWS Organizations SCP | **Yes** | No | Enforces organization-wide hard boundaries before API operations hit IAM evaluation. |
| **Activity Logging** | AWS CloudTrail | No | **Yes** | Captures immutable records of all API actions across every account for historical auditing. |
| **Compliance Baseline**| AWS Config | No | **Yes** | Continually evaluates resource configurations against organizational compliance rules. |
| **Posture Aggregation**| AWS Security Hub | No | **Yes** | Consolidates security findings across AWS tools into a standardized compliance dashboard. |
| **Threat Detection** | AWS GuardDuty | No | **Yes** | Applies machine learning to VPC Flow Logs, DNS queries, and CloudTrail data to flag active threats. |

---

## 2. Implementation & Enforcement Layer

### 2.1 Preventative Guardrails
Preventative controls are enforced globally at the **ROOT** and individual **OU nodes** via Service Control Policies (SCPs). They intercept actions in flight and return an immediate AccessDenied error to any API client—including admin accounts—if a policy restriction is violated.

### 2.2 Detective Guardrails
Detective controls process asynchronous resource state changes. When an infrastructure transformation occurs:
1. **AWS CloudTrail** records the source identity, timestamp, and payload.
2. **AWS Config** snapshots the new state, verifying compliance rules (e.g., confirming if an S3 bucket configuration matches public-access-block = true).
3. If an anomaly is identified, an alert is transmitted to **AWS Security Hub** and dispatched to central operations for programmatic remediation.
