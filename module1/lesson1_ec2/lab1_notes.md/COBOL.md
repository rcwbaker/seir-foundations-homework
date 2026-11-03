## COBOL practice

**Run used:** Run X  
**Instance ID:** i-XXXXXXXXXXXXXXXXX  
**Folder:** `/opt/balerica-bank`

### Return code 0 — success (`cobol_rc0.jpg`)

```text
$ ./cobol/bin/payment_post TXN-XX-0001 100001 125.50 USD INV-1001
PASTE EXACT OUTPUT HERE
$ echo $?
0
```

### Return code 4 — account not found (`cobol_rc4.jpg`)

```text
$ ./cobol/bin/account_lookup 999999
PASTE EXACT OUTPUT HERE
$ echo $?
4
```

### Return code 8 — business rejection (`cobol_rc8.jpg`)

```text
$ ./cobol/bin/payment_post TXN-XX-0002 100001 0.00 USD INV-1002
PASTE EXACT OUTPUT HERE
$ echo $?
8
```

### Return code 12 — environment failure (`cobol_rc12.jpg`)

```text
$ cd ~
$ /opt/balerica-bank/cobol/bin/account_lookup 100001
PASTE EXACT OUTPUT HERE
$ echo $?
12
```

### Ledger decoded by hand (`cobol_ledger_decode.jpg`)

| Columns | Field | Command | Value |
|---|---|---|---|
| 1-6 | Account ID | `cut -c1-6 data/accounts.dat` | |
| 7-36 | Customer name | `cut -c7-36 data/accounts.dat` | |
| 37-44 | Status | `cut -c37-44 data/accounts.dat` | |
| 45-56 | Balance | `cut -c45-56 data/accounts.dat` | |
| 57-59 | Currency | `cut -c57-59 data/accounts.dat` | |

**Alice's balance decoded:** raw field `XXXXXXXXXXXX` becomes `$XXXX.XX` (the decimal point is implied before the last 2 digits).

### My journal lines

```text
PASTE YOUR OWN TXN-XX-#### LINES FROM data/payments.dat HERE
```

**Did the balance change?** Yes / No. Explain in 1 to 2 sentences, with Alice's balance before and after.
