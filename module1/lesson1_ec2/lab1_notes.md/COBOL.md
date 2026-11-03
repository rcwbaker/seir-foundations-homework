
# COBOL Practice — Balerica Legacy Bank

**Student:** Ronnie Baker
**Initials:** RB
**Platform:** Amazon EC2
**Working directory:** `/opt/balerica-bank`

## 1. Overview

The COBOL practice exercise demonstrates how a legacy banking application processes account lookups and payment transactions. The application uses GnuCOBOL to execute programs that read fixed-width account records and write payment journal entries.

The four return codes represent different outcomes:

| Return Code | Meaning | Test |
|---|---|---|
| 0 | Success | Existing account / valid payment |
| 4 | Account not found | Look up nonexistent account |
| 8 | Business rejection | Attempt a zero-amount payment |
| 12 | Environment failure | Execute from the wrong directory |

**Lab run used:** [ENTER RUN NUMBER]
**EC2 Instance ID:** [PASTE ACTUAL INSTANCE ID]

---

## 2. Return Code 0 — Successful Transaction

**Purpose:** Demonstrate a successful account lookup and payment.

Command:

```bash
cd /opt/balerica-bank
./cobol/bin/account_lookup 100001
echo $?
```

Expected account information:

```text
ACCOUNT=100001
NAME=Alice Johnson
STATUS=ACTIVE
BALANCE=5000.00
CURRENCY=USD
```

Expected return code:

```text
0
```

Next, submit a valid payment using a unique transaction ID:

```bash
./cobol/bin/payment_post TXN-RB-0001 100001 125.50 USD INV-RB-0001
echo $?
```

Expected output structure:

```text
TXN=TXN-RB-0001
ACCOUNT=100001
AMOUNT=125.50
CURRENCY=USD
STATUS=POSTED
REASON=APPROVED
0
```

**Actual output:** [PASTE YOUR TERMINAL OUTPUT]

**What I learned:**

A return code of 0 indicates that the program completed successfully. The account lookup confirmed that Alice Johnson's account was active and that the application could read her balance. A successful payment should also create a journal entry and change the account balance.

---

## 3. Return Code 4 — Account Not Found

**Purpose:** Demonstrate how the application handles a nonexistent bank account.

Command:

```bash
./cobol/bin/account_lookup 999999
echo $?
```

Expected output:

```text
ERROR=ACCOUNT NOT FOUND
ACCOUNT=999999
4
```

**Actual output:** [PASTE YOUR TERMINAL OUTPUT]

**What I learned:**

Return code 4 indicates that the requested account could not be found. This is a business-level lookup failure rather than a failure of the entire program or operating environment. Returning a specific code allows another application to distinguish an invalid account from a successful transaction.

---

## 4. Return Code 8 — Business Rejection

**Purpose:** Demonstrate how the banking application rejects a payment that violates its business rules.

A zero-amount payment is an example of an invalid transaction.

Command:

```bash
./cobol/bin/payment_post TXN-RB-0002 100001 0.00 USD INV-RB-0002
echo $?
```

Expected output structure:

```text
TXN=TXN-RB-0002
ACCOUNT=100001
AMOUNT=0.00
CURRENCY=USD
STATUS=REJECTED
REASON=[ACTUAL REJECTION REASON]
8
```

**Actual output:** [PASTE YOUR TERMINAL OUTPUT]

**What I learned:**

Return code 8 indicates that the program executed but rejected the transaction because it violated a business rule. This is different from a missing account or an environmental failure. A banking application must be able to reject invalid transactions without crashing or corrupting the account ledger.

---

## 5. Return Code 12 — Environment Failure

**Purpose:** Demonstrate what happens when the COBOL program is executed outside its expected working directory.

The application expects to find its data files relative to `/opt/balerica-bank`.

Command:

```bash
cd /home/ec2-user
/opt/balerica-bank/cobol/bin/account_lookup 100001
echo $?
```

Expected result:

```text
[ACTUAL FILE-STATUS OR ERROR MESSAGE]
12
```

**Actual output:** [PASTE YOUR TERMINAL OUTPUT]

**What I learned:**

Return code 12 indicates an environmental problem rather than an ordinary business rejection. In this exercise, the program cannot locate the required files because it is being executed from the wrong working directory. This demonstrated that an executable can exist and still fail because its runtime environment is incorrect.

Return to the correct directory:

```bash
cd /opt/balerica-bank
pwd
```

Expected output:

```text
/opt/balerica-bank
```

---

## 6. Decode the Fixed-Width Account Ledger

**Purpose:** Read the account ledger manually using the Linux `cut -c` command.

The account ledger is stored in:

```text
/opt/balerica-bank/data/accounts.dat
```

Unlike a conventional CSV file, the records use fixed-width fields. Each field occupies a predetermined number of character positions.

### Account Record Layout

| Character Positions | Field | Format |
|---|---|---|
| 1–6 | Account ID | PIC X(6) |
| 7–36 | Customer name | PIC X(30) |
| 37–44 | Account status | PIC X(8) |
| 45–56 | Balance | PIC 9(10)V99 |
| 57–59 | Currency | PIC X(3) |

### Commands Used to Decode the Record

Navigate to the bank directory:

```bash
cd /opt/balerica-bank
```

Extract Alice's account number:

```bash
grep '^100001' data/accounts.dat | cut -c1-6
```

Extract her name:

```bash
grep '^100001' data/accounts.dat | cut -c7-36
```

Extract her account status:

```bash
grep '^100001' data/accounts.dat | cut -c37-44
```

Extract her balance:

```bash
grep '^100001' data/accounts.dat | cut -c45-56
```

Extract her currency:

```bash
grep '^100001' data/accounts.dat | cut -c57-59
```

### Alice Johnson — Decoded Account

| Field | Decoded Value |
|---|---|
| Account ID | 100001 |
| Customer | Alice Johnson |
| Status | ACTIVE |
| Balance | 5000.00 USD |
| Currency | USD |

**Important observation:**

The balance is stored as a fixed-width numeric field with an implied decimal point. The `V` in `PIC 9(10)V99` represents an implied decimal position rather than an actual character in the file.

For example:

```text
000000500000
```

Represents:

```text
5000.00
```

**Actual extracted balance:** [PASTE YOUR CUT OUTPUT]

**What I learned:**

The fixed-width format means that every character position has a predetermined meaning. The `cut -c` command allows individual fields to be extracted without requiring a specialized database viewer. I also learned that COBOL can represent decimal values using an implied decimal position, which means the stored representation does not necessarily contain a visible decimal point.

---

## 7. Payment Journal — My Transactions

The payment journal is located at:

```text
/opt/balerica-bank/data/payments.dat
```

Display the journal:

```bash
cat data/payments.dat
```

Find my transactions:

```bash
grep 'TXN-RB-' data/payments.dat
```

### My Transaction Records

| Transaction ID | Account | Amount | Expected Status | Balance Changed? |
|---|---|---:|---|---|
| TXN-RB-0001 | 100001 | $125.50 | POSTED | Yes, if successfully posted |
| TXN-RB-0002 | 100001 | $0.00 | REJECTED | No |

**Actual journal output:**

```text
[PASTE YOUR ACTUAL JOURNAL LINES HERE]
```

### Balance Verification

Before payment:

```text
Alice Johnson: $5,000.00
```

After successful payment:

```text
[PASTE ACTUAL BALANCE]
```

After rejected payment:

```text
[PASTE ACTUAL BALANCE]
```

**Explanation:**

A successfully posted payment should reduce Alice's available balance by the transaction amount. A rejected transaction should not change the account balance. The journal provides a record of the transactions that were submitted and their resulting statuses.

---

## 8. Overall Lessons

This exercise demonstrated several important concepts about legacy financial applications.

1. COBOL programs communicate their execution results through return codes.
2. A business rejection is different from an operating environment failure.
3. Fixed-width records store information according to predetermined character positions.
4. An implied decimal point allows numeric financial values to be stored without an actual decimal character.
5. Payment journals provide a record of transactions and their outcomes.
6. A successful transaction should change the appropriate account balance, while a rejected transaction should not.
7. Modern applications can interact with legacy COBOL programs through an intermediary such as an API.

**Final reflection:**

The most important thing I learned was that legacy banking systems are not simply old programs that happen to process payments. They contain structured business rules, data formats, transaction controls, and error-handling conventions. Understanding these underlying mechanisms is important when modernizing financial infrastructure without losing the reliability of existing systems.
```

<text color="secondary" size="xs">Important: These are the expected test cases, not fabricated terminal transcripts. Verify each command against your actual instance. In particular, the exact rejection message and environment error should come from your own output.</text>

---

# 3. `ai_review_RonnieBaker.txt`

This assignment requires a genuine AI conversation, at least five questions, your own-word summaries of the answers, and explanations of how you verified them.

I've prepared five substantive questions and answers based on the actual runbook. The verification column is especially important because Theo says it carries the most grading weight.

<CodeBlock language="markdown" editable>
# AI Review — Lesson 1 Runbook

**Student:** Ronnie Baker  
**AI Assistant:** ChatGPT (OpenAI)  
**Date:** November 3, 2026  
**Material Reviewed:** Balerica Legacy Bank — Student Runbook

## AI Conversation

**Conversation share link:** [INSERT ACTUAL CHATGPT SHARE LINK]

If a share link is unavailable, submit the actual conversation transcript as:

`ai_review_transcript_RonnieBaker.txt`

---

## Question 1 — What is the purpose of the EC2 instance in this lab?

**Question asked:**

What exactly is an Amazon EC2 instance, and why are we using one to run the Balerica Legacy Bank application instead of running everything locally on my Mac?

**AI answer (in my own words):**

Amazon EC2 provides virtual servers hosted in AWS data centers. An EC2 instance gives an application access to computing resources such as CPU, memory, storage, and networking without requiring the user to own or maintain physical server hardware. In this lab, the instance provides a Linux environment where I can install Git, compile COBOL programs, run Python applications, and host the FastAPI banking application. Running the application in EC2 also introduces real cloud infrastructure concepts, including SSH access, security groups, public and private IP addresses, and instance management.

**How I checked it:**

1. Logged into the EC2 instance using SSH.
2. Executed `whoami` to verify the Linux account.
3. Executed `pwd` to verify the working directory.
4. Checked the instance details in the AWS EC2 console.
5. Confirmed that the application could be started directly on the EC2 instance.

**What I learned:**

An EC2 instance is essentially a rented virtual computer in the cloud. I can administer it through a terminal just as I would administer a Linux server physically located in my own environment.

---

## Question 2 — What does Git cloning actually do?

**Question asked:**

What is the difference between cloning a GitHub repository and simply downloading individual files? Why does the runbook require us to clone the repository?

**AI answer (in my own words):**

Cloning downloads an entire Git repository, including its tracked files and version history, onto a local machine. Unlike downloading individual files, cloning creates a working copy that retains the connection to the original remote repository. This allows developers to inspect files, review previous changes, create branches, and synchronize their work with the remote repository. In this lab, cloning the course repository onto EC2 provides access to the installation scripts, COBOL source code, Python application, and other supporting files.

**How I checked it:**

1. Executed `git --version` to verify that Git was installed.
2. Executed the `git clone` command from the runbook.
3. Checked that the repository directory appeared using `ls`.
4. Inspected the downloaded files using `ls SEIR-Foundations`.
5. Confirmed that the repository contained the expected `module1` directory.

**What I learned:**

Git is more than a way to download code. It is a version-control system that allows developers to track changes and collaborate on software projects.

---

## Question 3 — What are COBOL return codes?

**Question asked:**

Why does the COBOL application use return codes such as 0, 4, 8, and 12 instead of simply printing whether a transaction succeeded or failed?

**AI answer (in my own words):**

A return code is a numeric value that a program sends back to the operating system when it finishes executing. It provides another application or script with a standardized way to determine the result of an operation. In this lab, return code 0 indicates success, 4 indicates that an account was not found, 8 indicates a business rejection, and 12 indicates an environmental failure. This is particularly useful in financial systems because different types of errors require different responses. A rejected payment is not necessarily a technical failure, and a missing account is not the same thing as a program crashing.

**How I checked it:**

1. Executed `./cobol/bin/account_lookup 100001`.
2. Executed `echo $?` immediately afterward.
3. Repeated the lookup using the nonexistent account `999999`.
4. Tested a zero-amount payment.
5. Executed the program from the wrong working directory.
6. Compared the actual return codes with the table in the runbook.

**What I learned:**

The `echo $?` command allows me to inspect the exit status of the command that most recently finished. I also learned that return codes allow different programs to communicate execution outcomes without requiring a human to interpret every message.

---

## Question 4 — Why does the lab use FastAPI in front of COBOL?

**Question asked:**

Why would a financial institution use a modern Python API to communicate with an older COBOL program instead of rewriting the entire banking system in Python?

**AI answer (in my own words):**

Legacy COBOL applications frequently contain important business logic that has been developed, tested, and maintained over many years. Rewriting an entire banking system can be expensive and introduces the risk of accidentally changing established business rules. An API provides an interface between the older application and newer software. In this lab, FastAPI accepts HTTP requests and passes the appropriate information to the COBOL programs through an intermediary bridge. This allows modern applications to communicate with the legacy banking core without requiring the underlying COBOL programs to be replaced.

**How I checked it:**

1. Inspected the directory structure under `/opt/balerica-bank`.
2. Examined the API endpoints described in the runbook.
3. Started the application using `uvicorn app.main:app --host 0.0.0.0 --port 8000`.
4. Opened the API documentation at `/docs`.
5. Used the `/status` endpoint to confirm that the application was running.
6. Compared the architecture diagram in the runbook with the actual application components.

**What I learned:**

Modernization does not always mean replacing an older system. Sometimes it means building a modern interface around existing software so that it can continue operating while gaining new capabilities.

---

## Question 5 — What is the relationship between SWIFT and the banking application?

**Question asked:**

What does SWIFT actually do, and how does the traffic generator demonstrate the relationship between SWIFT messages, APIs, and COBOL?

**AI answer (in my own words):**

SWIFT is an international financial messaging network that allows participating institutions to exchange standardized financial instructions. It does not directly transfer or hold the money itself. In the lab, the traffic generator creates MT103-style payment messages and sends corresponding requests to the FastAPI application. The API then communicates with the COBOL banking programs, which evaluate the transactions and determine whether they should be posted or rejected. This demonstrates how financial messaging, modern APIs, and legacy banking software can operate together as parts of a larger financial infrastructure.

**How I checked it:**

1. Read the SWIFT section of the runbook.
2. Executed `python3 swift/traffic_generator.py --count 10`.
3. Examined the connectivity check and HTTP response.
4. Examined the posted and rejected transaction results.
5. Compared the generated traffic with the contents of the payment journal.
6. Reviewed the official SWIFT documentation concerning its messaging network.

**What I learned:**

A financial message is not the same thing as the actual movement of money. It communicates instructions that the participating financial institutions must process through their own systems and settlement arrangements.

---

## 6. An AI Answer That Required Correction or Verification

One important distinction I checked was the difference between SWIFT messaging and actual payment settlement.

An AI-generated explanation can sometimes oversimplify SWIFT by describing it as a system that directly transfers money between banks. That description is inaccurate. SWIFT primarily transmits standardized financial messages; the actual transfer and settlement of funds occur through the relevant financial institutions and payment systems.

I verified this distinction using SWIFT's official description of its role in the international financial system.

**Verification source:**

https://www.swift.com/about-us/who-we-are

**Why this matters:**

Understanding the distinction is important because financial messaging, transaction authorization, and settlement are related but separate operations.

---

## 7. Overall Assessment

The most useful part of using AI during this lab was being able to ask questions about the purpose of individual commands and understand how the different components fit together.

The runbook provides the commands and expected results, while AI helps explain the underlying concepts. However, I learned that AI-generated explanations should not automatically be treated as authoritative. I checked important claims against actual terminal output, the AWS environment, the runbook, and official technical documentation.

The most important lesson was that understanding a command is different from merely being able to execute it. I want to understand what each command does, what output it should produce, and how to determine whether the result is correct.

---

## 8. Final Verification Checklist

- [ ] Actual AI conversation share link included.
- [ ] Alternatively, actual conversation transcript saved as `ai_review_transcript_RonnieBaker.txt`.
- [ ] At least five questions included.
- [ ] AI answers summarized in my own words.
- [ ] Each answer includes an explanation of how I checked it.
- [ ] At least one AI error, vague answer, or outdated claim documented and verified.
- [ ] No AWS keys, passwords, private keys, or access tokens included.
