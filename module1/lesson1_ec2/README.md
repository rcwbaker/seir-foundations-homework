# Lesson 1 — EC2 Lab Runs

**Student:** Ronnie Baker  
**Time zone:** America/Chicago  
**Week:** 3 (Assigned Tue 10/27/26, Due Tue 11/03/26 12:00 PM CST)  
**Runbook:** [Balerica Legacy Bank — Student Runbook](https://github.com/BalericaAI/SEIR-Foundations/blob/main/module1/lesson1_ec2/API/runbook.md)

## Lab Run Records

Every value below comes from the matching screenshot. Boot time is the
`uptime -s` output, which only printed when the ID line used lowercase
`ec2-metadata -i`. Public IPv4 DNS is the us-east-1 DNS name for the public IP
shown in each screenshot's Instance Connect footer.

| Run | Date | Time zone | Instance ID | Boot time (UTC) | Public IPv4 DNS | Screenshot | Terminated? |
|---|---|---|---|---|---|---|---|
| 1 | 11/3/2026 (10:17 CST) | America/Chicago | `i-09293f801f284eab6` | Not shown (`ec2-metadata -I` error) | `ec2-34-228-70-74.compute-1.amazonaws.com` | [lab1_run1.jpg](Lab%20Runs/lab1_run1.jpg) | Yes |
| 2 | 11/3/2026 (06:57 CST) | America/Chicago | `i-02990f8ea4604f0c2` | `2026-11-03 12:45:08` | `ec2-3-94-64-81.compute-1.amazonaws.com` | [lab1_run2.jpg](Lab%20Runs/lab1_run2.jpg) | Yes |
| 3 | 11/3/2026 (07:47 CST) | America/Chicago | `i-073b76f479bd6b380` | `2026-11-03 13:20:11` | `ec2-54-165-83-218.compute-1.amazonaws.com` | [lab1_run3.jpg](Lab%20Runs/lab1_run3.jpg) | Yes |
| 4 | 11/3/2026 (09:09 CST) | America/Chicago | `i-00205a422f3b2d368` | Not shown (`ec2-metadata -I` error) | `ec2-100-53-135-200.compute-1.amazonaws.com` | [lab1_run4.jpg](Lab%20Runs/lab1_run4.jpg) | Yes |
| 5 | 11/3/2026 (09:26 CST) | America/Chicago | `i-06a9d25f07d289d7e` | Not shown (`ec2-metadata -I` error) | `ec2-54-152-108-73.compute-1.amazonaws.com` | [lab1_run5.jpg](Lab%20Runs/lab1_run5.jpg) | Yes |
| 6 | 11/3/2026 (09:43 CST) | America/Chicago | `i-03169f2b54f5fed28` | Not shown (`ec2-metadata -I` error) | `ec2-23-20-112-188.compute-1.amazonaws.com` | [lab1_run6.jpg](Lab%20Runs/lab1_run6.jpg) | Yes |
| 7 | 11/3/2026 (10:01 CST) | America/Chicago | `i-09129f1856aff12f6` | `2026-11-03 15:48:53` | `ec2-3-91-60-9.compute-1.amazonaws.com` | [lab1_run7.jpg](Lab%20Runs/lab1_run7.jpg) | Yes |

Terminated: checked on 11/9/2026 in AWS Global View. There were no running
instances in any region and no leftover volumes in us-east-1.

Per-run notes, mistakes, commands and the COBOL practice section are in
[lab1_notes.md](lab1_notes.md).

## Submission checklist

| Item | File | Status |
|---|---|---|
| 7 lab-run screenshots | `Lab Runs/lab1_run1.jpg` – `lab1_run7.jpg` | ⚠️ All 7 on one day (limit is 3 per day). Runs 1, 4, 5, 6 lack instance ID + boot time in the ID line. |
| Lab notes | [lab1_notes.md](lab1_notes.md) | ✅ Real per-run notes, mistakes, and commands |
| COBOL rc 0 / rc 4 | shown in every lab-run screenshot | ⚠️ Separate `cobol_rc0.jpg` / `cobol_rc4.jpg` not yet taken |
| COBOL rc 8 / rc 12 / ledger decode | `cobol_rc8.jpg`, `cobol_rc12.jpg`, `cobol_ledger_decode.jpg` | ❌ Not done |
| Git clone screenshot | `git_clone.jpg` | ❌ Not done |
| AI review | [ai_review_RonnieBaker.txt](ai_review_RonnieBaker.txt) | ⚠️ Needs the real conversation share link or transcript |
| Spotter | [spotter_RonnieBaker.txt](spotter_RonnieBaker.txt) | ⚠️ Needs the name of the person I spotted and a cross-check with both people |
| AI-enabled study | [AI_enabled_study_lab1.0.txt](AI_enabled_study_lab1.0.txt) | ✅ |
| Udemy quizzes | `Udemy/Maarek_Section21_quiz.jpg`, `23`, `25` | ✅ |
| BAM extra credit | — | Not attempted |
