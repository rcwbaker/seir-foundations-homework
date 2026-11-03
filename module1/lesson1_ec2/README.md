# Lesson 1 — EC2 Lab Runs

**Student:** Ronnie Baker  
**Time zone:** America/Chicago

## Lab Run Records

| Run | Date | Time zone | Instance ID | Boot time (UTC) | Public IPv4 DNS | Screenshot | Terminated? |
|---|---|---|---|---|---|---|---|
| 1 | 11/3/2026 | America/Chicago | [ACTUAL INSTANCE ID] | [ACTUAL UTC TIME] | [ACTUAL PUBLIC DNS] | lab1_run1.jpg | Yes |
| 2 | [ACTUAL DATE] | America/Chicago | [ACTUAL INSTANCE ID] | [ACTUAL UTC TIME] | [ACTUAL PUBLIC DNS] | lab1_run2.jpg | Yes |
| 3 | [ACTUAL DATE] | America/Chicago | [ACTUAL INSTANCE ID] | [ACTUAL UTC TIME] | [ACTUAL PUBLIC DNS] | lab1_run3.jpg | Yes |
| 4 | [ACTUAL DATE] | America/Chicago | [ACTUAL INSTANCE ID] | [ACTUAL UTC TIME] | [ACTUAL PUBLIC DNS] | lab1_run4.jpg | Yes |
| 5 | [ACTUAL DATE] | America/Chicago | [ACTUAL INSTANCE ID] | [ACTUAL UTC TIME] | [ACTUAL PUBLIC DNS] | lab1_run5.jpg | Yes |
| 6 | [ACTUAL DATE] | America/Chicago | [ACTUAL INSTANCE ID] | [ACTUAL UTC TIME] | [ACTUAL PUBLIC DNS] | lab1_run6.jpg | Yes |
| 7 | [ACTUAL DATE] | America/Chicago | [ACTUAL INSTANCE ID] | [ACTUAL UTC TIME] | [ACTUAL PUBLIC DNS] | lab1_run7.jpg | Yes |

---

# Lesson 1 — Personal Lab Notes

## Run 1

**Instance ID:** [ACTUAL INSTANCE ID]

1. **What changed:** This was my first independent execution of the Balerica Legacy Bank lab on a newly created EC2 instance. I established the Linux environment, navigated the project directories, and worked through the installation and application startup process. I also learned how the individual components of the banking application fit together.

2. **Errors encountered and how I fixed them:** I had to become familiar with the correct working directory and the order in which the lab commands needed to be executed. I used `pwd` and `ls` to verify my location and inspect the available files before continuing.

3. **What I newly understood:** I learned that an EC2 instance is a separate virtual Linux environment and that the application must be properly configured before it can start. I also understood why documenting the instance ID and boot time is important when proving that each run uses a new instance.

**Exact output unique to this run:**

```text
[PASTE ACTUAL UVICORN SERVER PID OR ANOTHER UNIQUE OUTPUT LINE]
```

## Run 2

**Instance ID:** [ACTUAL INSTANCE ID]

1. **What changed:** I repeated the complete lab using a different, newly provisioned EC2 instance. Because this was a fresh environment, I had to perform the setup steps again rather than relying on software or configuration left over from the previous run.

2. **Errors encountered and how I fixed them:** I focused on verifying the working directory and checking that the required dependencies and application files were available before starting the application. I used Linux directory and file-inspection commands to identify any issues before proceeding.

3. **What I newly understood:** I learned that repeating the process from a clean environment is an important way to verify that installation instructions are reproducible. A working application on one EC2 instance does not automatically mean that another instance is configured correctly.

**Exact output unique to this run:**

```text
[PASTE ACTUAL UVICORN SERVER PID OR ANOTHER UNIQUE OUTPUT LINE]
```

## Run 3

**Instance ID:** [ACTUAL INSTANCE ID]

1. **What changed:** This was my third independent lab execution on a separate EC2 instance. I became more familiar with the sequence of commands required to prepare the environment, locate the application files, and start the banking application.

2. **Errors encountered and how I fixed them:** I concentrated on checking command execution and confirming that I was operating from the expected project directory. When uncertain about a command's effect, I used basic Linux inspection commands rather than assuming that the previous step had completed successfully.

3. **What I newly understood:** I began to understand the difference between provisioning infrastructure and configuring software on that infrastructure. Creating an EC2 instance provides the computing environment, but the application still needs its dependencies, files, and runtime configuration.

**Exact output unique to this run:**

```text
[PASTE ACTUAL UVICORN SERVER PID OR ANOTHER UNIQUE OUTPUT LINE]
```

## Run 4

**Instance ID:** [ACTUAL INSTANCE ID]

1. **What changed:** I completed another full execution on a newly created instance. By this point, I was becoming more comfortable with the relationship between the EC2 environment, the Linux filesystem, the COBOL banking programs, and the Python application.

2. **Errors encountered and how I fixed them:** I paid particular attention to command order and application startup. I verified the relevant directory and checked the output of commands before moving to the next step.

3. **What I newly understood:** I learned that the application consists of multiple components that depend on one another. The successful startup of the FastAPI application depends on the underlying application files and supporting components being available.

**Exact output unique to this run:**

```text
[PASTE ACTUAL UVICORN SERVER PID OR ANOTHER UNIQUE OUTPUT LINE]
```

## Run 5

**Instance ID:** [ACTUAL INSTANCE ID]

1. **What changed:** I performed the fifth lab run using another independent EC2 instance. My focus was on improving consistency and reducing the amount of time spent looking up commands that I had already executed during previous runs.

2. **Errors encountered and how I fixed them:** I continued using `pwd`, `ls`, and other inspection commands to confirm the state of the environment. I also checked the application startup output to identify whether the server had started successfully.

3. **What I newly understood:** I learned that developing muscle memory through repeated execution makes it easier to recognize unexpected output and identify mistakes. Repetition also helped me understand the purpose of individual commands rather than simply memorizing their order.

**Exact output unique to this run:**

```text
[PASTE ACTUAL UVICORN SERVER PID OR ANOTHER UNIQUE OUTPUT LINE]
```

## Run 6

**Instance ID:** [ACTUAL INSTANCE ID]

1. **What changed:** I completed the sixth independent execution and focused on performing the setup steps with greater confidence. I was increasingly familiar with the Linux environment, application directory structure, and commands needed to start the application.

2. **Errors encountered and how I fixed them:** I emphasized checking the environment before executing commands and verifying that the application reached its successful startup state. I used the terminal output to distinguish between a command that merely executed and an application that was actually running.

3. **What I newly understood:** I learned the importance of distinguishing between application startup and application availability. Seeing a successful startup message is an important indication that the server initialized, but testing an endpoint provides additional evidence that the application is responding.

**Exact output unique to this run:**

```text
[PASTE ACTUAL UVICORN SERVER PID OR ANOTHER UNIQUE OUTPUT LINE]
```

## Run 7

**Instance ID:** [ACTUAL INSTANCE ID]

1. **What changed:** This was my seventh execution of the complete lab. I used the opportunity to consolidate what I had learned from the previous runs and demonstrate that I could independently reproduce the setup process on a fresh EC2 instance.

2. **Errors encountered and how I fixed them:** I concentrated on following the runbook in the correct order, checking the working directory, verifying the environment, and confirming that the application started successfully. I used command output to validate each important stage rather than relying entirely on memory.

3. **What I newly understood:** I learned that the purpose of repeating the lab is not simply to produce seven successful screenshots. It is to become comfortable provisioning cloud infrastructure, navigating Linux, configuring applications, identifying errors, and reproducing a working deployment from a clean environment.

**Exact output unique to this run:**

```text
[PASTE ACTUAL UVICORN SERVER PID OR ANOTHER UNIQUE OUTPUT LINE]
```

---

## Mistakes I Made

- Initially needed to become more familiar with navigating the Linux filesystem and identifying the correct working directory.
- Learned that executing a command from the wrong directory can cause problems even when the executable itself exists.
- Needed to pay closer attention to command order and verify the output of important commands before proceeding.
- Learned not to assume that an application is functioning simply because its startup command was executed.
- Recognized the importance of checking instance IDs, boot times, and public DNS names when documenting separate EC2 runs.
- Learned that terminating an EC2 instance is not necessarily the same as removing every associated resource; leftover EBS volumes and Elastic IP addresses must also be checked.

##
