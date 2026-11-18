# CGE-P Lab 3.3 – Writing Compliance Policies in Rego (GCP)

## Overview

This lab is part of my hands-on journey through **AJ Yawn’s CGE-P GRC Engineering course**. Lab 3.3 focuses on using **Rego and Policy as Code** to translate compliance requirements into automated, testable policies for GCP resources.

The core workflow:

**Requirement → Rego Policy → Evaluation → Finding → Remediation → Re-test → Evidence**

## Policy Files by Cloud

This folder holds two sets of policies. The GCP set came from Lab 3.3, and the AWS set (the `*_aws.rego` files) was added in Lab 3.4. Each AWS file covers the same NIST 800-53 control as its GCP counterpart and has its own package name, so both sets can be evaluated side by side.

| Control | GCP (Lab 3.3) | AWS (Lab 3.4) | What it checks |
|---|---|---|---|
| AC-3 Access Enforcement | [ac3_no_public.rego](ac3_no_public.rego) (`compliance.ac3`) | [ac3_no_public_aws.rego](ac3_no_public_aws.rego) (`compliance.ac3_aws`) | **GCP:** GCS buckets enforce uniform bucket-level access and public access prevention, and firewall rules don't open 22/3389 to `0.0.0.0/0`. **AWS:** every S3 bucket has an `aws_s3_bucket_public_access_block` with all four flags set to `true`. |
| CM-6 Configuration Settings | [cm6_required_tags.rego](cm6_required_tags.rego) (`compliance.cm6`) | [cm6_required_tags_aws.rego](cm6_required_tags_aws.rego) (`compliance.cm6_aws`) | **GCP:** storage buckets, compute instances and disks carry the labels `project`, `environment`, `managed_by` and `compliance_scope`. **AWS:** S3 buckets, DynamoDB tables, Lambda functions, KMS keys and CloudTrail trails carry the tags `Project`, `Environment`, `ManagedBy` and `ComplianceScope`. |
| SC-28 Encryption at Rest | [sc28_encryption.rego](sc28_encryption.rego) (`compliance.sc28`) | [sc28_encryption_aws.rego](sc28_encryption_aws.rego) (`compliance.sc28_aws`) | **GCP:** GCS buckets use a customer-managed encryption key (CMEK). **AWS:** every S3 bucket has a matching `aws_s3_bucket_server_side_encryption_configuration`. |

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