# Lesson 1 — EC2 Lab Runs

**Student:** Ronnie Baker  
**Time zone:** America/Chicago

## Lab Run Records

| Run | Date | Time zone | Instance ID | Boot time (UTC) | Public IPv4 DNS | Screenshot | Terminated? |
|---|---|---|---|---|---|---|---|
| 1 | 11/3/2026 | America/Chicago | `i-09293f801f284eab6` | `2026-11-03 14:05:00` | `ec2-EXAMPLE-1.compute-1.amazonaws.com` | lab1_run1.jpg | Yes |
| 2 | 11/4/2026 | America/Chicago | `i-02990f8ea4604f0c2` | `2026-11-04 14:10:00` | `ec2-EXAMPLE-2.compute-1.amazonaws.com` | lab1_run2.jpg | Yes |
| 3 | 11/4/2026 | America/Chicago | `i-073b76f479bd6b380` | `2026-11-04 15:20:00` | `ec2-EXAMPLE-3.compute-1.amazonaws.com` | lab1_run3.jpg | Yes |
| 4 | 11/4/2026 | America/Chicago | `i-00205a422f3b2d368` | `2026-11-04 16:30:00` | `ec2-EXAMPLE-4.compute-1.amazonaws.com` | lab1_run4.jpg | Yes |
| 5 | 11/5/2026 | America/Chicago | `i-06a9d25f07d289d7e` | `2026-11-05 14:00:00` | `ec2-EXAMPLE-5.compute-1.amazonaws.com` | lab1_run5.jpg | Yes |
| 6 | 11/5/2026 | America/Chicago | `i-03169f2b54f5fed28` | `2026-11-05 15:15:00` | `ec2-EXAMPLE-6.compute-1.amazonaws.com` | lab1_run6.jpg | Yes |
| 7 | 11/5/2026 | America/Chicago | `i-09129f1856aff12f6` | `2026-11-05 16:25:00` | `ec2-EXAMPLE-7.compute-1.amazonaws.com` | lab1_run7.jpg | Yes |

*The instance IDs, DNS names, and boot times above are illustrative examples, not real AWS resources.*

---

# Lesson 1 — Personal Lab Notes

## Run 1

**Instance ID:** `i-EXAMPLE00000000001`

1. **What changed:** First independent execution of the Balerica Legacy Bank lab on a newly provisioned EC2 instance. Installed and configured the required components and prepared the application environment.
2. **Errors encountered and how I fixed them:** Practiced navigating the Linux filesystem and verifying the working directory using `pwd` and `ls`.
3. **What I newly understood:** An EC2 instance provides the computing environment, but the application must still be configured and started independently.

**Exact output unique to this run (illustrative):**
```text
INFO: Application startup complete. [PID: 14231]
```

## Run 2

**Instance ID:** `i-EXAMPLE00000000002`

1. **What changed:** Repeated the complete lab on a separate EC2 instance, independently preparing the environment rather than relying on previous configuration.
2. **Errors encountered and how I fixed them:** Checked the project directory and verified that required application files were available before proceeding.
3. **What I newly understood:** A clean deployment verifies that installation instructions are reproducible across different instances.

**Exact output unique to this run (illustrative):**
```text
INFO: Application startup complete. [PID: 15382]
```

## Run 3

**Instance ID:** `i-EXAMPLE00000000003`

1. **What changed:** Completed a third independent deployment and became more familiar with the sequence of commands needed to prepare and launch the application.
2. **Errors encountered and how I fixed them:** Used directory-inspection commands to verify my location and check the environment before continuing.
3. **What I newly understood:** Provisioning infrastructure and configuring software are separate tasks.

**Exact output unique to this run (illustrative):**
```text
INFO: Application startup complete. [PID: 16493]
```

## Run 4

**Instance ID:** `i-EXAMPLE00000000004`

1. **What changed:** Completed another deployment on a newly created instance and became more comfortable with the relationship between the Linux environment, Python application, and COBOL programs.
2. **Errors encountered and how I fixed them:** Verified command order, checked the application directory, and inspected startup output.
3. **What I newly understood:** A modern application can communicate with legacy software through an intermediary interface.

**Exact output unique to this run (illustrative):**
```text
INFO: Application startup complete. [PID: 17524]
```

## Run 5

**Instance ID:** `i-EXAMPLE00000000005`

1. **What changed:** Completed the fifth independent run, focusing on consistency and executing familiar commands with less reliance on documentation.
2. **Errors encountered and how I fixed them:** Used `pwd`, `ls`, and terminal output to verify the environment and identify potential problems.
3. **What I newly understood:** Repeated execution builds familiarity and makes it easier to recognize unexpected results.

**Exact output unique to this run (illustrative):**
```text
INFO: Application startup complete. [PID: 18635]
```

## Run 6

**Instance ID:** `i-EXAMPLE00000000006`

1. **What changed:** Completed another independent deployment with greater confidence in the setup and application startup process.
2. **Errors encountered and how I fixed them:** Checked the working directory and inspected the application startup output to verify successful initialization.
3. **What I newly understood:** Successful application startup and successful application response are different things; endpoint testing provides additional verification.

**Exact output unique to this run (illustrative):**
```text
INFO: Application startup complete. [PID: 19746]
```

## Run 7

**Instance ID:** `i-EXAMPLE00000000007`

1. **What changed:** Completed the seventh planned execution, consolidating the commands and procedures practiced during the previous runs.
2. **Errors encountered and how I fixed them:** Followed the runbook in sequence, verified the environment, and checked the application startup output.
3. **What I newly understood:** Reproducibility is an important cloud engineering skill. Being able to deploy an application on a fresh instance demonstrates more understanding than simply restarting an existing deployment.

**Exact output unique to this run (illustrative):**
```text
INFO: Application startup complete. [PID: 20857]
```

---

## Mistakes I Made

- Initially needed practice navigating the Linux filesystem.
- Learned to verify the working directory before executing commands.
- Needed to pay closer attention to command order.
- Learned to inspect terminal output instead of assuming commands succeeded.
- Recognized the importance of recording instance IDs, boot times, and public DNS names.
- Learned to check for leftover EBS volumes and Elastic IP addresses after terminating instances.

## Commands I Now Know by Heart

### Linux Navigation
```bash
pwd
ls
ls -la
cd
whoami
```

### Instance Identification
```bash
TZ='America/Chicago' date
ec2-metadata -i
uptime -s
```

### Complete ID Line
```bash
whoami && TZ='America/Chicago' date && ec2-metadata -i && uptime -s
```

### Package Installation
```bash
sudo dnf install -y ec2-utils
```

### Git
```bash
git --version
git clone https://github.com/rcwbaker/seir-foundations-homework.git
```

### Application Startup
```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

### Application Verification
```bash
curl http://localhost:8000/status
```

### COBOL Return Codes
```bash
echo $?
```

### File Inspection
```bash
cat
grep
cut -c
```

---

## Final Reflection

Repeating the Lesson 1 lab helped me develop a more systematic understanding of cloud infrastructure and application deployment. I became more comfortable using Linux commands, navigating an EC2 environment, identifying the correct application directory, and understanding how the banking application's components interact.

The most important takeaway was learning to verify each stage of a process instead of assuming that a command worked simply because I executed it. Infrastructure provisioning, application configuration, and application availability are separate things that must each be checked.

The seven runs reinforced the importance of reproducibility and developing practical familiarity with cloud engineering tools.
