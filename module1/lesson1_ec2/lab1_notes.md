# Lesson 1 — Lab Notes

**Student:** Ronnie Baker  
**Time zone:** America/Chicago  
**Region:** us-east-1

All seven runs were done on **Tuesday, November 3, 2026**. Every detail below
(times, instance IDs, PIDs, errors) is copied from the matching screenshot in
[`Lab Runs/`](Lab%20Runs/).

The runs are numbered by screenshot file name. Their actual order that morning
(CST) was: Run 2 (06:57) → Run 3 (07:47) → Run 4 (09:09) → Run 5 (09:26) →
Run 6 (09:43) → Run 7 (10:01) → Run 1 (10:17).

---

## Run 1 — `i-09293f801f284eab6` (Name tag: `mybank0`)

**What changed:** This was the last run of the morning (ID line at 10:17:24 CST),
on a new instance with private IP 172.31.19.128. I ran Steps 0–4 again:
`account_lookup 100001` (return code `0`), `account_lookup 999999` (return code
`4`), posted `TXN0001`, and started uvicorn.

**Errors and fixes:** I typed `ec2-metadata -I` with a capital I, so the ID line
printed `ec2-metadata: invalid option -- 'I'` and `Terminating...`. Because the
commands were chained with `&&`, `uptime -s` never ran either, so this
screenshot has no instance ID or boot time. I didn't catch it before starting
uvicorn. The fix is lowercase `-i`, which worked in Runs 2, 3 and 7.

**What I newly understood:** With `&&`, one failed command stops everything
after it, so one typo cost me two of the four ID-line outputs. The instance ID
is only visible in the EC2 Instance Connect footer, which the homework doesn't
count as the ID line.

**Output only this run produced:**
```text
INFO:     Started server process [35892]
```

---

## Run 2 — `i-02990f8ea4604f0c2` (Name tag: `mybank`)

**What changed:** This was the first run of the day. The ID line printed at
06:57:45 CST, and `uptime -s` showed a boot time of `2026-11-03 12:45:08` UTC,
about 13 minutes earlier. Private IP was 172.31.24.243.

**Errors and fixes:** The ID line worked the first time, with all four parts
(`ec2-user`, the CST date, `instance-id: i-02990f8ea4604f0c2`, the boot
time). The account lookups returned `0` and `4` as expected, and
`payments.dat` held exactly one `TXN0001` line.

**What I newly understood:** `date` is in my time zone (CST, UTC−6) but
`uptime -s` is in the server's UTC. 12:45 UTC is 06:45 CST, which is how I know
the instance booted 13 minutes before the screenshot.

**Output only this run produced:**
```text
instance-id: i-02990f8ea4604f0c2
2026-11-03 12:45:08
INFO:     Started server process [36030]
```

---

## Run 3 — `i-073b76f479bd6b380` (Name tag: `myapp`)

**What changed:** Second run of the day. The ID line printed at 07:47:21 CST,
with boot time `2026-11-03 13:20:11` UTC (07:20 CST), about 27 minutes earlier.
Private IP was 172.31.24.189. This instance had a different Name tag (`myapp`)
from the others.

**Errors and fixes:** No errors. The full ID line printed and uvicorn reached
`Application startup complete.`

**What I newly understood:** Every new instance gets a new instance ID, private
IP and public IP. That's how the homework can tell seven runs apart, and why
restarting one instance wouldn't count.

**Output only this run produced:**
```text
instance-id: i-073b76f479bd6b380
2026-11-03 13:20:11
INFO:     Started server process [36715]
```

---

## Run 4 — `i-00205a422f3b2d368` (Name tag: `mybank2`)

**What changed:** Third run of the day (09:09:04 CST), private IP
172.31.16.15. `cat data/payments.dat` showed **two** identical `TXN0001` lines, so
`payment_post TXN0001 ...` ran twice on this instance.

**Errors and fixes:** This is where the capital `-I` typo first appeared:
`ec2-metadata: invalid option -- 'I'`, so no instance ID or boot time. The
duplicate journal line shows `payment_post` accepted the same transaction ID
twice instead of rejecting it as a duplicate.

**What I newly understood:** The journal is append-only. Running a payment
twice writes it twice, and in a real bank that would be a double charge. That's
why transaction IDs need to be unique, and why the homework asks for my own
`TXN-RB-` IDs.

**Output only this run produced:**
```text
TXN0001              100001000000012550USDPOSTED  INV-1001
TXN0001              100001000000012550USDPOSTED  INV-1001
INFO:     Started server process [37015]
```

---

## Run 5 — `i-06a9d25f07d289d7e` (Name tag: `mybank3`)

**What changed:** Fourth run of the day (09:26:07 CST), private IP
172.31.27.84.

**Errors and fixes:** Two errors in one ID line. A stray `1` got pasted along
with the command, so bash printed `-bash: 1: command not found`, and the capital
`-I` typo happened again. I still started uvicorn, so this screenshot has no
instance ID or boot time.

**What I newly understood:** Bash runs every line I paste, including a stray
character like `1`. I need to look at what I pasted before pressing Enter.

**Output only this run produced:**
```text
-bash: 1: command not found
INFO:     Started server process [36007]
```

---

## Run 6 — `i-03169f2b54f5fed28` (Name tag: `mybank4`)

**What changed:** Fifth run of the day (09:43:36 CST), private IP
172.31.31.137.

**Errors and fixes:** Same two mistakes as Run 5: the pasted `1`
(`-bash: 1: command not found`) and `ec2-metadata -I`. No instance ID or boot
time in this screenshot.

**What I newly understood:** The same typo showed up in three runs in a row
(Runs 4, 5 and 6) before Run 7 got it right. A mistake I don't notice gets
repeated, so I need to read the ID line output every time before moving on.

**Output only this run produced:**
```text
INFO:     Started server process [35655]
```

---

## Run 7 — `i-09129f1856aff12f6` (Name tag: `mybank5`)

**What changed:** Sixth run of the day (10:01:17 CST), private IP 172.31.16.10.
I went back to lowercase `-i` and the full ID line worked.

**Errors and fixes:** No errors. The ID line printed `instance-id:
i-09129f1856aff12f6` and boot time `2026-11-03 15:48:53` UTC (09:48 CST),
about 12 minutes before the screenshot.

**What I newly understood:** A good screenshot shows the date, instance ID and
boot time together, with boot time before the screenshot time and within 24
hours. This one does. Runs 1, 4, 5 and 6 don't.

**Output only this run produced:**
```text
instance-id: i-09129f1856aff12f6
2026-11-03 15:48:53
INFO:     Started server process [35953]
```

---

## Mistakes I made

1. **`ec2-metadata -I` instead of `-i`** in Runs 1, 4, 5 and 6. Flags are case-sensitive, and the error stopped `uptime -s` too.
2. **Pasted a stray `1`** with the ID line in Runs 5 and 6 (`-bash: 1: command not found`).
3. **Posted `TXN0001` twice** in Run 4, which put a duplicate line in the payment journal.
4. **Started uvicorn without checking the ID line output** first, so four screenshots are missing the instance ID and boot time.
5. **Did all seven runs on one day (Nov 3).** The homework allows at most 3 per day across at least 3 days.
6. **Used the runbook's `TXN0001`** instead of my own `TXN-RB-` transaction IDs.

## Commands I now know by heart

```bash
whoami && TZ='America/Chicago' date && ec2-metadata -i && uptime -s   # the ID line (lowercase -i)
sudo dnf install -y git
git clone https://github.com/BalericaAI/SEIR-Foundations.git
bash SEIR-Foundations/module1/lesson1_ec2/API/install/install.sh
cd /opt/balerica-bank
./cobol/bin/account_lookup 100001        # return code 0
./cobol/bin/account_lookup 999999        # return code 4
echo $?                                  # return code of the last command
./cobol/bin/payment_post TXN0001 100001 125.50 USD INV-1001
cat data/payments.dat
source venv/bin/activate
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

---

## COBOL practice

**Instance used:** `i-0d9215c7ed93430d6` (Name tag `balerica-cobol-practice`),
launched 11/10/2026, boot time `2026-11-10 12:41:23` UTC, in
`/opt/balerica-bank`. This was a separate practice instance, not one of the
seven lab runs in the README table. Claude Code ran the terminal for this
session at my request. It was terminated afterwards.

Screenshots are in [`COBOL/`](COBOL/). Each one starts with the ID line.

### Return code 0 — success ([cobol_rc0.jpg](COBOL/cobol_rc0.jpg))
```text
$ ./cobol/bin/account_lookup 100001; echo $?
ACCOUNT=100001
NAME=Alice Johnson
STATUS=ACTIVE
BALANCE=5000.00
CURRENCY=USD
0
$ ./cobol/bin/payment_post TXN-RB-0001 100001 125.50 USD INV-RB-0001; echo $?
TXN=TXN-RB-0001
ACCOUNT=100001
AMOUNT=125.50
CURRENCY=USD
STATUS=POSTED
REASON=APPROVED
0
```

### Return code 4 — account not found ([cobol_rc4.jpg](COBOL/cobol_rc4.jpg))
```text
$ ./cobol/bin/account_lookup 999999; echo $?
ERROR=ACCOUNT NOT FOUND
ACCOUNT=999999
4
```

### Return code 8 — business rejection ([cobol_rc8.jpg](COBOL/cobol_rc8.jpg))
```text
$ ./cobol/bin/payment_post TXN-RB-0002 100001 0.00 USD INV-RB-0002; echo $?
TXN=TXN-RB-0002
ACCOUNT=100001
AMOUNT=0.00
CURRENCY=USD
STATUS=REJECTED
REASON=AMOUNT MUST BE GREATER THAN ZERO
8
```
The program ran fine and said no: the account exists and is active, but a
$0.00 payment breaks a business rule. That's a different failure from a missing
account (4) or a broken environment (12).

### Return code 12 — environment failure ([cobol_rc12.jpg](COBOL/cobol_rc12.jpg))
```text
$ cd ~ && pwd
/home/ec2-user
$ /opt/balerica-bank/cobol/bin/account_lookup 100001; echo $?
ERROR=CANNOT OPEN data/accounts.dat
FILE-STATUS=35
12
```
The program looks for `data/accounts.dat` relative to the **current folder**,
so running the same binary from `/home/ec2-user` can't find the file.
COBOL file status `35` means "file not found". The account is fine. The
environment is what's wrong.

### Ledger decoded by hand ([cobol_ledger_decode.jpg](COBOL/cobol_ledger_decode.jpg))
```text
$ grep '^100001' data/accounts.dat | cat -A
100001Alice Johnson                 ACTIVE  000000500000USD$
ID=[100001] NAME=[Alice Johnson                 ] STATUS=[ACTIVE  ] BALANCE=[000000500000] CCY=[USD]
```

| Columns (`cut -c`) | Field | Raw value | Meaning |
|---|---|---|---|
| 1–6 | Account ID | `100001` | 100001 |
| 7–36 | Name | `Alice Johnson` + 17 spaces | Alice Johnson |
| 37–44 | Status | `ACTIVE` + 2 spaces | ACTIVE |
| 45–56 | Balance `PIC 9(10)V99` | `000000500000` | **5000.00** (last 2 digits are cents, so there's no decimal point in the file) |
| 57–59 | Currency | `USD` | USD |

`cat -A` puts a `$` at the end of each line, which shows the record is exactly
59 characters with no tabs or commas. The padding spaces are part of the data.

### My journal lines
```text
$ grep TXN-RB data/payments.dat
TXN-RB-0001         100001000000012550USDPOSTED  INV-RB-0001
TXN-RB-0002         100001000000000000USDREJECTEDINV-RB-0002
$ ./cobol/bin/account_lookup 100001 | grep BALANCE
BALANCE=5000.00
```

**Did the balance change?** No. Alice's balance was still `5000.00` after
`TXN-RB-0001` (125.50) was POSTED. `payment_post` opens `accounts.dat` for
INPUT only and only appends a verdict to `payments.dat`. The COBOL core
approves or rejects payments but never updates the stored balance. The
rejected `TXN-RB-0002` was also written to the journal (as `REJECTED`, amount
`000000000000`), so the journal keeps rejections too, not just successes.

---

## Git clone ([git_clone.jpg](git_clone.jpg))

Same instance (`i-0d9215c7ed93430d6`), 11/10/2026 06:46:49 CST. Clone only:
no token on the server, nothing pushed.
```text
$ git clone https://github.com/rcwbaker/seir-foundations-homework.git
Cloning into 'seir-foundations-homework'...
Receiving objects: 100% (698/698), 13.18 MiB | 50.00 MiB/s, done.
$ ls seir-foundations-homework/module1
lab0.5_basics_contd  lab0_basics  lesson1_ec2  lesson2_slack
```

---

## BAM (extra credit)

Not attempted. The three `BAM_2.x.jpg` files in the old folder were empty
1-byte placeholders, so I removed them.
