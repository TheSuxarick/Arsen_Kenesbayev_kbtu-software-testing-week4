# Defect Reports

*Note: As permitted by the assignment guidelines, all three defects below are mock defects designed to demonstrate reporting structure. Environments, test data, and reproducibility values are illustrative.*

## Defect 1: Late SMS Code Processing
* **Title:** SMS Confirmation: Transfer executes successfully when correct code is entered after the 120-second expiration.
* **Environment:** iOS 18.2, app 4.11.0 build 2291, test env 2.
* **Preconditions:** Test customer TC-014, balance 1,000,000 KZT, daily total 0. Transfer of 150,000 KZT initiated, user is on the SMS screen.
* **Steps to reproduce:**
  1. Wait for exactly 125 seconds.
  2. Enter the correct SMS code received on the device.
  3. Tap Confirm.
* **Expected result:** System rejects the code as expired (timeout) and cancels the transfer.
* **Actual result:** System accepts the code and executes the transfer, debiting the account.
* **Reproducibility:** 5 of 5 attempts.
* **Severity:** High (Security and business logic violation).
* **Priority:** High.
* **Evidence:** Screen recording + request ID.
* **Traces to:** REQ-3.3 / TR-SMS-004

## Defect 2: Boundary Value Error on 100,000 KZT
* **Title:** Transfer Amount: SMS code screen appears unexpectedly for an exact 100,000 KZT transfer.
* **Environment:** Android 14, app 4.11.0 build 2291, test env 2.
* **Preconditions:** Test customer TC-015, balance 500,000 KZT, daily total 0.
* **Steps to reproduce:**
  1. Open Transfers -> Between my accounts.
  2. Enter exactly 100,000.
  3. Tap Continue.
* **Expected result:** Transfer executes immediately without asking for an SMS code (requirement states SMS is for > 100,000 KZT).
* **Actual result:** The SMS code screen appears.
* **Reproducibility:** 5 of 5 attempts.
* **Severity:** Low (Functional inconvenience, but no data loss).
* **Priority:** Medium.
* **Evidence:** Screenshot.
* **Traces to:** REQ-3.3 / TR-DAY-004

## Defect 3: Requirement Ambiguity on Midnight Boundary
* **Title:** Daily Limits: Unclear handling of daily total calculation for transfers crossing midnight.
* **Environment:** Backend Service, test env 2.
* **Preconditions:** Test customer TC-016, balance 2,000,000 KZT. Yesterday's daily total: 900,000 KZT. System time is 23:59.
* **Steps to reproduce:**
  1. Initiate a transfer of 150,000 KZT at 23:59:50.
  2. Wait until system time changes to 00:00:10 (the next day).
  3. Enter the correct SMS code and tap Confirm.
* **Expected result:** The requirement (REQ-3.2) lacks specific business rules for transfers spanning two calendar days. It is expected that the system consistently applies the limit based on either initiation or confirmation time.
* **Actual result:** Transfer is rejected with a "Daily limit exceeded" error message, indicating the limit is tied to initiation time, blocking valid next-day operations.
* **Reproducibility:** 3 of 3 attempts.
* **Severity:** Medium (Edge case preventing valid operations due to requirement gap).
* **Priority:** Medium.
* **Evidence:** Backend logs, request ID.
* **Traces to:** REQ-3.2