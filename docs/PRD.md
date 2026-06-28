
## Project Name

**CloudSchema Diff** _(working title)_

---

# 1. Overview

CloudSchema Diff is a semantics-based comparator which is meant to help DevOps specialists validate cloud infrastructure migrations through comparing configurations of different cloud service providers. The tool does not perform direct comparisons of configuration files but normalizes the resources of various providers to a unified semantics model in order to find functional similarities and differences.

The task here is not cloud infrastructure management, but helping engineers understand if two clouds represent the same infrastructure.

---

# 2. Target Users

### Primary Users

- DevOps Engineers
    
- Cloud Engineers
    
- Cloud Architects
    

### Secondary Users

- Companies migrating workloads between cloud providers
    
- Students and researchers learning cloud interoperability
    

---

# 3. Problem Statement

Cloud vendors use different terms, data models, and configuration frameworks when describing similar infrastructures.

Therefore, engineers moving between cloud vendors may find themselves at odds when trying to determine whether two particular configurations are the same. This can lead to security, performance, and configuration problems.

---

# 4. Product Goal

The tool provides a systematic and understandable framework that allows engineers to compare various cloud settings and see if they can be considered equal infrastructure settings. The application should answer the following questions:

- Are these two resources equivalent?
    
- If not, what are the differences?
    
- What impact could these differences have?
    

---

# 5. Scope (MVP)

Version 1 supports comparison of:

### Supported Resource Categories

- Compute Resources
    
- Network Access
    

Examples include:

- EC2 ↔ Azure Virtual Machine
    
- Security Group ↔ Network Security Group
    

The application compares only the supported resource types.

Unsupported resources should be clearly reported instead of being analyzed incorrectly.

---

# 6. Out of Scope

The MVP will **not**:

- Deploy infrastructure
    
- Modify cloud resources
    
- Connect directly to AWS accounts
    
- Connect directly to Azure accounts
    
- Connect to GCP
    
- Generate Terraform code
    
- Support Kubernetes
    
- Support every cloud service
    
- Use AI or Large Language Models for comparison
    

---

# 7. Inputs

The user uploads two cloud configuration files representing infrastructure from two cloud providers.

Example:

- AWS configuration
    
- Azure configuration
    

---

# 8. Expected Output

The application generates a comparison report containing:

### Overall Summary

- Overall compatibility score
    
- Number of resources compared
    
- Number of equivalent resources
    
- Number of partially equivalent resources
    
- Number of non-equivalent resources
    

### Detailed Resource Comparison

For every supported resource:

- Resource type
    
- Cloud provider resource
    
- Equivalent resource
    
- Comparison status
    
- Attribute differences
    
- Explanation of detected differences
    
- Potential impact
    

Example:

Compute Resource

Status:  
Partially Equivalent

Differences:

- CPU: 4 → 2
    
- Public IP: Enabled → Disabled
    

Potential Impact:

- Reduced processing capacity
    
- Resource will no longer be publicly accessible
    

---

# 9. Semantic Equivalence

The comparison engine evaluates the **meaning** of resources rather than their names.

A resource may be considered:

### Equivalent

The resources represent the same semantic concept and have matching relevant attributes.

Example:

AWS EC2

↓

Azure Virtual Machine

↓

Canonical Concept: Compute Resource

↓

Equivalent

---

### Partially Equivalent

The resources represent the same semantic concept but differ in one or more important attributes.

Example:

Both are Compute Resources

but

CPU:  
4 vs 2

Result:  
Partially Equivalent

---

### Not Equivalent

The resources represent different semantic concepts or have incompatible configurations that significantly change their behavior.

Example:

Public Internet Access

vs

Private Internal Access

Result:  
Not Equivalent

---

### Unsupported

The application has no semantic mapping for the uploaded resource type.

Rather than guessing, the application reports the resource as unsupported.

---

# 10. Unique Value Proposition

Unlike traditional configuration comparison tools that compare files syntactically, CloudSchema Diff performs semantic comparison using a provider-independent canonical model.

The application delivers:

- Structured comparison
    
- Repeatable analysis
    
- Explainable results
    
- Human-readable impact assessment
    

without relying on artificial intelligence.

---

# 11. Success Criteria

The MVP is considered successful if a user can:

1. Upload two cloud configurations.
    
2. Compare supported resources.
    
3. Understand whether resources are equivalent.
    
4. Identify important configuration differences.
    
5. Understand the practical impact of those differences through clear explanations.