# CGE-P Lab 3.3 – Writing Compliance Policies in Rego (GCP)

## Overview

This lab is part of my hands-on journey through **AJ Yawn’s CGE-P GRC Engineering course**. Lab 3.3 focuses on using **Rego and Policy as Code** to translate compliance requirements into automated, testable policies for GCP resources.

The core workflow:

**Requirement → Rego Policy → Evaluation → Finding → Remediation → Re-test → Evidence**

## Initial Findings

The initial policy evaluation identifies cloud configurations that do not meet the defined security requirements. Areas evaluated may include:

- 🔐 Encryption and key-management requirements
- 🔑 IAM and access-control configurations
- ⚙️ Secure configuration baselines
- 🪣 Cloud storage security settings

A failed policy check becomes a **finding that requires investigation and remediation**.

## Remediation

For each finding:

1. **Identify** the configuration that failed the Rego policy.
2. **Understand the risk** associated with the failure.
3. **Update the infrastructure/configuration** to meet the requirement.
4. **Commit the change** to version control for traceability.
5. **Re-run the Rego policy** to verify remediation.
6. **Confirm PASS** and retain the results as evidence.

### Before Remediation

`Rego Policy → FAIL → Finding`

### After Remediation

`Configuration Updated → Commit → Rego Policy → PASS`

## Key Takeaway

The biggest lesson from this lab was seeing how compliance requirements can become **executable policies**.

Instead of relying only on screenshots and manual reviews:

> **The requirement informs the policy. The Rego code performs the test. The commit provides traceability. The passing result becomes part of the evidence.**

This is another step toward moving from **documenting compliance to continuously testing and engineering compliance**.

## Disclaimer

This repository documents my personal CGE-P lab work and learning experience. It does not reproduce proprietary course instructions or protected training materials.