# ☁️ Lab: Security Network Architecture with VPCs

### 📋 Scenario
I joined **Cymbal Bank** as a Junior Cloud Security Analyst. The organization is migrating to a hybrid cloud environment and requires a secure, isolated network structure to extend their on-premises data center.

**My Mission:** Architect a test environment to assess security configurations before live deployment. This involves defining network boundaries using Virtual Private Clouds (VPCs) rather than using the insecure "Default" network.

### 🎯 Objectives
* Provision a custom **Virtual Private Cloud (VPC)** to isolate traffic.
* Define specific **Subnets** to segment network resources.
* Verify network architecture using **Google Cloud Shell (CLI)**.

### 🛠️ Technologies Used
* **Google Cloud Platform (GCP)**
* **Cloud Shell** (Linux/Bash environment)
* **gcloud SDK** (Command Line Interface)

---

### 🚀 Steps Taken

#### 1. Create the Custom VPC
Instead of using the GUI, I used the CLI to ensure repeatable Infrastructure as Code (IaC). I created a custom VPC with automatic subnet creation **disabled** to enforce strict control over IP ranges.

```bash
gcloud compute networks create cymbal-test-vpc \
    --subnet-mode=custom \
    --bgp-routing-mode=regional
```


#### 2. Configure the Secure Subnet
I carved out a specific CIDR block (10.10.10.0/24) for the security testing team. This ensures that resources in this subnet are logically separated from other bank operations.

```bash
gcloud compute networks subnets create security-test-subnet \
    --network=cymbal-test-vpc \
    --range=10.10.10.0/24 \
    --region=us-east1
```

#### 3. Network Verification
After provisioning, I verified the architecture to ensure no unauthorized default subnets were created.

Listing all networks to confirm isolation:

```bash
gcloud compute networks list
``````
