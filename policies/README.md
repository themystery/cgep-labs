CGE-P Lab 3.3 – Writing Compliance Policies in Rego (GCP)
Overview
This lab is part of my hands-on journey through AJ Yawn's Certified GRC Engineer – Practitioner (CGE-P) course.
Lab 3.3: Writing Compliance Policies in Rego (GCP) focuses on moving beyond manually reviewing cloud configurations and learning how compliance requirements can be translated into machine-readable policy using Rego.
The objective is to identify security and compliance issues within Google Cloud Platform (GCP) infrastructure, write Rego policies that detect those conditions, review the resulting findings, remediate the underlying configuration, and validate that the resource now satisfies the defined policy.
The key lesson from this lab is simple:
If a compliance requirement can be clearly defined, portions of its technical validation can often be expressed and tested as code.


Lab Objectives
The lab demonstrates how a GRC professional can:
- Understand the fundamentals of Rego and Policy as Code.
- Translate security requirements into testable policy logic.
- Evaluate GCP infrastructure against defined compliance requirements.
- Identify noncompliant configurations as findings.
- Connect technical findings to security risk.
- Remediate infrastructure rather than simply documenting the deficiency.
- Re-run policy checks to validate remediation.
- Create repeatable compliance evidence through code and automated evaluation.

Why Rego?
Traditional compliance assessments often require an assessor or ISSO to manually review configurations and supporting evidence to determine whether a control requirement has been satisfied.
Rego introduces another layer to this process.
Instead of relying exclusively on a human to repeatedly ask:
"Does this resource meet the security requirement?"
we can define logic that allows tooling to continuously evaluate specific technical requirements.
The workflow becomes:
Requirement → Policy → Evaluation → Finding → Remediation → Re-evaluation → Evidence
This does not eliminate human judgment. Instead, it allows repeatable technical checks to be automated so GRC professionals can spend more time evaluating risk, context, exceptions, and control effectiveness.

Initial Findings
During the initial compliance evaluation, the goal is to identify GCP configurations that do not satisfy the security requirements represented by the Rego policies.
Examples of findings that may be evaluated in a GCP policy-as-code exercise include the following.
Finding 1 – Storage Resource Does Not Meet Required Security Configuration
Observation:
A cloud storage resource may be deployed without one or more required security settings.
Risk:
Inadequate storage configuration can increase the possibility of unauthorized access, data exposure, or inconsistent implementation of the organization's security baseline.
Expected State:
Storage resources should inherit or explicitly implement the approved security configuration.
Remediation:
Update the underlying infrastructure configuration to implement the required security settings and redeploy the resource.
Validation:
Re-run the Rego policy against the updated configuration and confirm that the original violation is no longer returned.

Finding 2 – Access Controls Are Too Permissive
Observation:
IAM permissions or resource access configurations may allow access beyond the intended users, groups, or service accounts.
Risk:
Excessive privileges increase the attack surface and may allow unauthorized users or services to access protected cloud resources.
Remediation:
- Remove unnecessary permissions.
- Apply least privilege.
- Limit IAM roles to required identities.
- Avoid overly broad or public access where it is not explicitly required.
- Re-evaluate the resource against the Rego policy.
Desired Result:
Only authorized identities retain the minimum permissions required to perform their functions.

Finding 3 – Encryption Requirements Are Not Satisfied
Observation:
A resource may not meet the organization's defined encryption or cryptographic key-management requirements.
Risk:
Sensitive information may not receive the level of protection required by the organization's security baseline.
Remediation:
- Apply the required encryption configuration.
- Configure the appropriate key-management mechanism.
- Restrict access to cryptographic keys.
- Implement key rotation where required.
- Validate the updated resource against the applicable policy.

Finding 4 – Required Configuration Baseline Is Missing
Observation:
A GCP resource may be deployed without configuration settings required by the approved security baseline.
Risk:
Configuration drift or inconsistent deployments can create security weaknesses between development, testing, and production environments.
Remediation:
Define the approved settings within Infrastructure as Code and enforce them consistently across environments.
Where practical, secure settings should become the default configuration rather than something teams must remember to add manually after deployment.

Remediation Workflow
The remediation process used throughout the lab follows a repeatable GRC Engineering approach:
1. Identify the Finding
Run the policy evaluation and determine which resource or configuration violates the defined requirement.
2. Understand the Risk
Do not stop at the policy failure.
Determine:
- What configuration failed?
- Why does the requirement exist?
- What threat or vulnerability does it address?
- What could happen if the finding remains unresolved?
This connects technical configuration to actual risk.
3. Update the Infrastructure
Modify the applicable GCP/Terraform configuration rather than simply documenting the finding.
This is where compliance begins moving closer to engineering.
4. Commit the Remediation
Commit the updated configuration and policy changes to version control.
The commit provides traceability into:
- What changed
- Why it changed
- When it changed
- Which configuration or policy was modified
The repository therefore becomes part of the compliance evidence trail.
5. Re-run the Policy
Evaluate the infrastructure again using the Rego policy.
A remediation should not be considered complete simply because the configuration was changed.
The updated state must be validated.
6. Confirm the Finding Is Resolved
Compare the original result with the post-remediation result.
Before:
Policy Evaluation → FAIL
After remediation:
Policy Evaluation → PASS
This provides stronger evidence that the identified configuration issue was addressed.

From Finding to Evidence
One of my biggest takeaways from this lab is how Policy as Code can change the traditional compliance workflow.
Traditional Approach
Control → Manual Review → Screenshot → Finding → Remediation → New Screenshot
GRC Engineering Approach
Control → Rego Policy → Automated Evaluation → Finding → Code Remediation → Commit → Re-evaluation → Evidence
The second approach provides greater repeatability, consistency, traceability, and scalability for technical controls that can be evaluated programmatically.

Initial Finding and Remediation Summary
Finding	Initial State	Remediation	Validation
Storage configuration	Noncompliant configuration detected	Apply required hardened configuration	Re-run Rego policy
IAM/access	Permissions exceed requirement	Apply least privilege	Policy returns compliant result
Encryption	Required protection not implemented	Configure approved encryption/key management	Validate configuration through policy
Configuration baseline	Required setting missing	Update IaC/security baseline	Re-evaluate deployed configuration
GRC Perspective
As an ISSO/GRC professional, the most valuable part of this exercise is not simply learning Rego syntax.
It is learning to think differently about control implementation and evidence.
Instead of only asking an engineer:
"Can you provide evidence that this control is implemented?"

GRC Engineering encourages another question:
"Can this requirement be expressed as policy and continuously evaluated?"

That distinction matters.
If the requirement can be evaluated programmatically, compliance testing can become more consistent and repeatable.
Human judgment is still necessary for determining risk, reviewing exceptions, understanding system context, evaluating compensating controls, and making authorization decisions.
But the repetitive technical validation can increasingly be automated.

Evidence Generated
Potential evidence from this lab includes:
- Rego policy files
- Terraform/GCP configuration
- Initial policy evaluation results
- Documented findings
- Remediation commits
- Updated infrastructure configuration
- Post-remediation policy results
- Version-control history
Together, these artifacts can tell a stronger compliance story than a standalone screenshot.
The policy defines what is expected.
The infrastructure code shows what should be deployed.
The commit provides change traceability.
The policy evaluation demonstrates whether the configuration satisfies the requirement.

Key Takeaways
This lab reinforced several concepts for me:
1. Controls can become executable requirements.
Where a requirement is technically measurable, Rego can help translate compliance expectations into testable policy logic.
2. Findings should lead to engineering changes.
The objective is not simply to document noncompliance. The goal is to identify the root configuration issue and remediate it.
3. Remediation requires validation.
Changing a configuration is not sufficient. The policy should be executed again to verify that the finding has actually been resolved.
4. Version control strengthens traceability.
Policies and infrastructure changes maintained in Git provide a history of how security requirements and implementations evolve.
5. Automation complements—not replaces—GRC judgment.
Rego can evaluate defined technical conditions, but GRC professionals still need to interpret risk, understand context, evaluate exceptions, and determine whether controls are effective.

Final Reflection
Lab 3.3 – Writing Compliance Policies in Rego (GCP) helped me connect another important piece of the GRC Engineering lifecycle.
Earlier labs demonstrated how security requirements can be incorporated into infrastructure.
This exercise takes the next step:
How do we automatically test whether those requirements are actually being followed?
That is where Policy as Code becomes powerful.
The control requirement informs the policy.
The Rego code defines the test.
The infrastructure is evaluated.
A failure becomes a finding.
The configuration is remediated.
The policy is executed again.
The result becomes part of the evidence.
For me, this represents the shift from simply documenting compliance toward engineering, testing, and continuously validating compliance.

Disclaimer
This repository documents my personal learning, implementation work, findings, and observations while progressing through the CGE-P course.
It does not reproduce proprietary course instructions, lab solutions, or protected training materials. Specific findings and remediation steps should be adapted to the actual resources, policies, and requirements being evaluated.