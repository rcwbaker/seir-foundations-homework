# Lesson 2 Homework — Seven Alerts, Seven Wins (Notes)

**Student:** Ronnie Baker  **Date:** Monday, Nov 9, 2026
**Instance:** `i-0772f55e42309ca3e` (`balerica-bank-slack`, us-east-1, Amazon Linux 2023, t3.micro)
**Slack:** `#balerica-alerts` in workspace `seirfoundatio-lih4040.slack.com`

> Rebuilt for this homework: a fresh EC2 instance → Lesson 1 installer
> (`install.sh`) → `slack.py` + `.env` (chmod 600, in `.gitignore`) →
> `python slack.py --test` → `SUCCESS: Chewbacca approves!`

---

## Run log — all seven scripts (every one: `Delivered!`)

| # | Script | Result |
|---|--------|--------|
| 1 | `hw1_hello_slack.py` | INFO "Hello from Ronnie!..." delivered (HW-001) |
| 2 | `hw2_severity_tour.py` | INFO, WARNING, ERROR, CRITICAL → all 4 DELIVERED |
| 3 | `hw3_server_time.py` | Server: *Monday November 09, 2026 at 22:53:47 UTC* |
| 4 | `hw4_disk_watch.py` | Disk 25.1% used → INFO, delivered |
| 5 | `hw5_load_check.py` | Load 0.07 / 0.05 / 0.07 on 2 CPUs → INFO, delivered |
| 6 | `hw6_incident_drill.py` ×3 | DRILL-7044 [WARNING] EOD batch +12 min · DRILL-6709 [INFO] backup OK · DRILL-8285 [CRITICAL] ledger unreachable |
| 7 | `hw7_morning_report.py` | Report delivered (22:54:18 UTC, disk 25.1%, load 0.17, Python 3.9.25) |

ID line (Lesson 1 format): `ec2-user` · `Mon Nov 9 16:54:18 CST 2026` · `instance-id: i-0772f55e42309ca3e`

---

## "In your notes:" answers

### hw2 — Which severities arrived, and WHY those?
**All four** arrived (INFO, WARNING, ERROR, CRITICAL) because `.env` had
`SLACK_ALERT_SEVERITY=INFO`. `slack.py` ranks the levels INFO=0, WARNING=1,
ERROR=2, CRITICAL=3, and skips anything ranked *below* the threshold. INFO is the
lowest, so nothing was filtered. With the class default `ERROR`, only ERROR and
CRITICAL would arrive.

### hw3 — How many hours apart are server time and your wall clock?
**6 hours.** The server said 22:53 UTC. My clock (Chicago, CST) said 16:53. Central
time is UTC−6 in November, after daylight saving ended Nov 1. Servers run on UTC so
logs from machines in different regions line up, and there are no daylight saving
jumps that would leave an hour missing or repeated.

### hw4 — Why is a quiet INFO here GOOD design, not a failure?
The disk is 25.1% used. That's healthy, so the code correctly picked INFO. Alerts
should mean "a human needs to act." If healthy readings paged people, they would learn
to ignore the channel (alert fatigue) and miss the real 90% ERROR. The monitor still
did its job: it measured, decided, and chose the right severity. Under an ERROR
threshold, staying silent is the correct result.

### hw5 — What would make this number spike on the Balerica bank?
Mine was 0.07 / 0.05 / 0.07 on 2 CPUs, which is basically idle. It would spike from:
- The end-of-day COBOL batch (`BATCH-EOD`) processing the day's transactions
- Payday, month-end, or holiday payment surges on the FastAPI `/payments` endpoint
- A SWIFT backlog being worked through all at once
- Nightly ledger backups and compression
- Compiling software (the GnuCOBOL build during install pegs the CPU)
- A runaway process or loop, or a traffic flood (bots or DDoS)

### hw6 — Which fake incidents deserve to wake a human at 3 AM?
I drew WARNING (DRILL-7044), INFO (DRILL-6709), and CRITICAL (DRILL-8285).
- **YES: CRITICAL** — `account_lookup` code 12, ledger file not reachable
  (DRILL-8285). Without the ledger, balances can't be looked up and money can't move.
- **YES: ERROR** — `/payments` 500s, or rejection rate above 5%. Real customers'
  payments are failing.
- **NO, review in the morning: WARNING** — EOD batch 12 minutes slow (DRILL-7044) or
  SWIFT queue at 42. Watch it, and escalate only if it keeps getting worse.
- **NEVER: INFO** — backup completed (DRILL-6709). Good news belongs in a report,
  not on a pager.

---

## Experiments

### Experiment 1 — `SLACK_ALERT_SEVERITY=CRITICAL`, rerun hw2
**Prediction:** 1 of 4 arrives (CRITICAL only).
**Result:**
```
INFO     -> skipped by your threshold
WARNING  -> skipped by your threshold
ERROR    -> skipped by your threshold
CRITICAL -> DELIVERED to Slack
```
**Prediction matched.** The filter runs *before* anything is sent, so the
skipped alerts never reached Slack.

### Experiment 2 — `SLACK_ALERTS_ENABLED=false`, run hw1
**Result:** `Skipped. Check .env: SLACK_ALERTS_ENABLED must be true...` and nothing
in Slack. `send_alert()` checks this flag first and returns `False` before it looks
at severity or contacts Slack.
**Why a kill switch helps:** during maintenance (patching, reboots, deploys) the
monitors would fire false alarms. One config line silences them with no code
change, and the same line turns them back on. No one gets paged for planned work.

### Experiment 3 — hw4 WARNING threshold 75 → 20 (below my 25.1%)
**Result:** `Disk is 25.1% used -> severity WARNING.` (it was INFO before). It was
delivered. Same disk, different decision: the threshold is a human engineering choice
written into code. Changed back to 75 afterwards.

### Experiment 4 — reset
Confirmed `SLACK_ALERTS_ENABLED=true`, `SLACK_ALERT_SEVERITY=INFO`, and hw4 back to `>= 75`. ✅

---

## Rules check
- All messages were synthetic. The webhook and `.env` contents never went to Slack, the notes, or the screenshots.
- No spam: each script ran once (hw6 three times), and the experiments sent 3 more messages.
- The `send_alert(agent, severity, message, incident_id)` interface was not changed.
