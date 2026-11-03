# AI Review of the Lesson 1 Runbook

**Student:** Ronnie Baker  
**AI used:** ChatGPT (OpenAI)  
**Conversation share link:** [INSERT ACTUAL CHATGPT SHARE LINK]  
*(Alternatively: transcript uploaded as `ai_review_transcript_RonnieBaker.txt`)*

## Question 1

**What I asked:**

What is the purpose of the ID line `whoami && TZ='America/Chicago' date && ec2-metadata -i && uptime -s`, and why does the homework require it in every screenshot?

**AI's answer (in my own words):**

The ID line establishes the identity and execution context of each lab run. `whoami` identifies the Linux user executing the commands, while `TZ='America/Chicago' date` displays the current date and time in my local time zone. `ec2-metadata -i` retrieves the EC2 instance ID, which uniquely identifies the virtual machine. Finally, `uptime -s` displays when the instance booted. Together, these commands provide evidence of who performed the work, when it was performed, which instance was used, and how long that instance had been running. This is particularly important because the homework requires seven separate runs using seven brand-new EC2 instances.

**How I checked it:**

1. Executed `whoami` and compared the result with my EC2 Linux username.
2. Executed `TZ='America/Chicago' date` and compared the displayed time with my local clock.
3. Executed `ec2-metadata -i` and compared the instance ID with the EC2 console.
4. Executed `uptime -s` and compared the boot time with the instance's launch information.
5. Repeated the complete ID line immediately before starting Uvicorn and confirmed that all four outputs appeared in the terminal.

## Question 2

**What I asked:**

Why does each of the seven lab runs require a brand-new EC2 instance? Why can't I simply restart the same instance seven times or use an instance created from a launch template?

**AI's answer (in my own words):**

Each run is intended to demonstrate that I can independently provision and configure a new EC2 environment and complete the lab steps manually. Reusing an existing instance would not demonstrate the same provisioning process because the machine could retain previously installed software, configuration changes, files, and other state from earlier runs. Restarting an instance does not create a new instance identity; it generally preserves the existing EC2 instance ID. The assignment also explicitly excludes instances created from baked launch templates or golden AMIs. Therefore, every qualifying run must use a separately created EC2 instance, with its own unique instance ID and public DNS name.

**How I checked it:**

1. Reviewed the homework instructions specifying seven brand-new instances.
2. Compared the instance IDs from different EC2 lab runs.
3. Checked the EC2 console to verify that each instance was a separate resource.
4. Confirmed that each run had a unique public IPv4 DNS name.
5. Checked the launch procedure to ensure that I was not using a baked AMI or launching from a preconfigured template.

## Question 3

**What I asked:**

What is the difference between a COBOL return code of 4, 8, and 12? Why are these considered different types of failures?

**AI's answer (in my own words):**

The return codes distinguish between different outcomes of the banking application. Return code 4 means that the requested account could not be found. Return code 8 indicates that the program encountered a business-rule rejection, such as attempting to process a payment with a zero amount. Return code 12 indicates an environmental failure, such as executing the program from the wrong working directory when required files cannot be located. These distinctions are important because a business rejection does not necessarily mean that the software itself malfunctioned. Similarly, an environmental failure is different from an invalid financial transaction. The return code allows another program or script to identify the type of outcome without having to interpret the entire error message.

**How I checked it:**

1. Executed the account lookup program using a nonexistent account number.
2. Immediately executed `echo $?` to inspect the return code.
3. Submitted a zero-amount payment using the payment-posting program.
4. Executed `echo $?` again to verify the business rejection.
5. Changed to an incorrect working directory and executed the program using its absolute path.
6. Compared the resulting return codes with the expected values in the homework instructions.

## Question 4

**What I asked:**

How does FastAPI communicate with the COBOL banking programs, and why would an organization use an API to modernize a legacy banking application instead of rewriting the entire application?

**AI's answer (in my own words):**

FastAPI provides a modern HTTP interface through which other applications can communicate with the underlying banking system. It accepts incoming requests, processes the information, and passes the appropriate operations to the COBOL programs through an intermediary bridge. COBOL then executes the established banking logic, including account lookups and payment processing. An organization might prefer this approach because a legacy banking application can contain decades of business rules and operational knowledge. Rewriting everything introduces considerable expense and the possibility of introducing errors into critical financial operations. An API allows an organization to make its existing software accessible to modern applications while preserving the underlying business logic.

**How I checked it:**

1. Inspected the Balerica Legacy Bank directory structure.
2. Examined the Python application and the COBOL program locations.
3. Started the FastAPI application using the Uvicorn command in the runbook.
4. Opened the interactive API documentation at `/docs`.
5. Tested the available health or status endpoint.
6. Compared the application architecture with the runbook's description of the COBOL bridge.

## Question 5

**What I asked:**

What is the difference between SWIFT and an API, and how does the Balerica Legacy Bank lab demonstrate their relationship?

**AI's answer (in my own words):**

SWIFT is an international financial messaging network that allows financial institutions to exchange standardized payment instructions. An API is an interface that allows different software applications to communicate with one another. They serve different purposes, even though they can work together. In the Balerica lab, the SWIFT traffic generator simulates financial payment messages and communicates with the banking application through HTTP requests. FastAPI receives those requests and passes the relevant transaction information to the COBOL banking programs. The COBOL programs then process the transactions and determine whether they should be accepted or rejected. This demonstrates how financial messaging, modern application interfaces, and legacy banking software can work together.

**How I checked it:**

1. Reviewed the SWIFT and API sections of the runbook.
2. Examined the traffic generator and its associated commands.
3. Ran the traffic generator according to the runbook's instructions.
4. Examined the HTTP responses returned by the API.
5. Compared the transaction results with the entries in the payment journal.
6. Consulted SWIFT's official website to verify that SWIFT primarily provides financial messaging rather than directly holding or transferring funds.

## Where the AI was wrong, vague, or out of date

**Question number:** 5

**What the AI said:**

An oversimplified explanation of SWIFT might describe it as a network that directly transfers money between banks.

**What was actually true:**

SWIFT primarily provides a secure, standardized messaging network through which financial institutions exchange payment instructions and other financial information. It does not itself hold customer deposits or directly settle the funds. Actual settlement takes place through the relevant financial institutions and payment systems. Messaging and settlement are related but distinct parts of an international payment.

**How I found out:**

I checked SWIFT's official website and compared its description of its role with the architecture described in the Balerica Legacy Bank runbook. This helped me distinguish between transmitting a payment instruction and actually settling the associated financial transaction.

Official reference: https://www.swift.com/about-us/who-we-are

---

*I did not paste any keys, passwords, or tokens into the AI.*
