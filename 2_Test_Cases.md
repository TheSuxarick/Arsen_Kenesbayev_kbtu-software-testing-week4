# Test Cases

## Group 1: Amount Limits (Traces to REQ-3.1)

**TR-AMT-001 | Below Minimum Amount**
* **Traces to:** REQ-3.1
* **Preconditions:** Test customer TC-01, balance 1,000,000 KZT, daily total 0 KZT.
* **Steps:**
  1. Open Transfers -> Between my accounts.
  2. Select the deposit account as recipient.
  3. Enter 99 and tap Continue.
* **Expected Result:** Transfer is rejected with an error message. Balance remains 1,000,000 KZT.

**TR-AMT-002 | Minimum Valid Amount**
* **Traces to:** REQ-3.1
* **Preconditions:** Test customer TC-02, balance 1,000,000 KZT, daily total 0 KZT.
* **Steps:**
  1. Open Transfers -> Between my accounts.
  2. Select the deposit account as recipient.
  3. Enter 100 and tap Continue.
* **Expected Result:** Transfer executes immediately. Balance becomes 999,900 KZT, daily total becomes 100 KZT.

**TR-AMT-003 | Maximum Valid Amount**
* **Traces to:** REQ-3.1
* **Preconditions:** Test customer TC-03, balance 1,000,000 KZT, daily total 0 KZT.
* **Steps:**
  1. Open Transfers -> Between my accounts.
  2. Select the deposit account as recipient.
  3. Enter 500,000 and tap Continue.
* **Expected Result:** SMS code screen appears. Transfer is not executed yet, daily total remains 0 KZT until confirmation.

**TR-AMT-004 | Above Maximum Amount**
* **Traces to:** REQ-3.1
* **Preconditions:** Test customer TC-04, balance 1,000,000 KZT, daily total 0 KZT.
* **Steps:**
  1. Open Transfers -> Between my accounts.
  2. Select the deposit account as recipient.
  3. Enter 500,001 and tap Continue.
* **Expected Result:** Transfer is rejected with an error message indicating the amount exceeds the maximum limit.

---

## Group 2: Daily Limits (Traces to REQ-3.2)

**TR-DAY-001 | Daily Limit Exceeded**
* **Traces to:** REQ-3.2
* **Preconditions:** Test customer TC-05, balance 2,000,000 KZT, daily total 900,000 KZT.
* **Steps:**
  1. Open Transfers -> Between my accounts.
  2. Select the deposit account as recipient.
  3. Enter 150,000 and tap Continue.
* **Expected Result:** Transfer is rejected with an error message indicating the daily limit is exceeded. 

**TR-DAY-002 | Valid Amount, Daily Limit OK, SMS Required**
* **Traces to:** REQ-3.2
* **Preconditions:** Test customer TC-06, balance 1,000,000 KZT, daily total 500,000 KZT.
* **Steps:**
  1. Open Transfers -> Between my accounts.
  2. Select the deposit account as recipient.
  3. Enter 200,000 and tap Continue.
* **Expected Result:** SMS code screen appears because the amount is >100,000 KZT.

**TR-DAY-003 | Valid Amount, Daily Limit OK, No SMS**
* **Traces to:** REQ-3.2
* **Preconditions:** Test customer TC-07, balance 1,000,000 KZT, daily total 500,000 KZT.
* **Steps:**
  1. Open Transfers -> Between my accounts.
  2. Select the deposit account as recipient.
  3. Enter 50,000 and tap Continue.
* **Expected Result:** Transfer executes immediately. Balance becomes 950,000 KZT, and daily total becomes 550,000 KZT.

**TR-DAY-004 | Exact Daily Limit Boundary**
* **Traces to:** REQ-3.2
* **Preconditions:** Test customer TC-08, balance 1,000,000 KZT, daily total 900,000 KZT.
* **Steps:**
  1. Open Transfers -> Between my accounts.
  2. Select the deposit account as recipient.
  3. Enter 100,000 and tap Continue.
* **Expected Result:** Transfer executes successfully. Daily total reaches exactly 1,000,000 KZT.

---

## Group 3: SMS Code State Transition (Traces to REQ-3.3)

**TR-SMS-001 | Correct SMS Code on First Attempt**
* **Traces to:** REQ-3.3
* **Preconditions:** Test customer TC-09, balance 1,000,000 KZT, daily total 0 KZT. User has initiated a 150,000 KZT transfer and is on the SMS code screen.
* **Steps:**
  1. Receive the SMS code on the mobile device.
  2. Enter the correct 4-digit code.
  3. Tap Confirm.
* **Expected Result:** Transfer is confirmed and executed. Balance becomes 850,000 KZT.

**TR-SMS-002 | Wrong Code Followed by Correct Code**
* **Traces to:** REQ-3.3
* **Preconditions:** Test customer TC-10, balance 1,000,000 KZT, daily total 0 KZT. User is on the SMS code screen for a 150,000 KZT transfer.
* **Steps:**
  1. Enter a wrong code (e.g., 1111) and tap Confirm.
  2. Clear the input, enter the correct code.
  3. Tap Confirm.
* **Expected Result:** First attempt shows an error. Second attempt is accepted, and the transfer is executed successfully.

**TR-SMS-003 | Blocked After 3 Wrong Attempts**
* **Traces to:** REQ-3.3
* **Preconditions:** Test customer TC-11, balance 1,000,000 KZT, daily total 0 KZT. User is on the SMS code screen for a 150,000 KZT transfer.
* **Steps:**
  1. Enter wrong code (1111) and tap Confirm.
  2. Enter wrong code (2222) and tap Confirm.
  3. Enter wrong code (3333) and tap Confirm.
* **Expected Result:** Transfer is blocked and cancelled after the 3rd attempt. Screen returns to the main menu with a failure message.

**TR-SMS-004 | 120 Seconds Expiration**
* **Traces to:** REQ-3.3
* **Preconditions:** Test customer TC-12, balance 1,000,000 KZT, daily total 0 KZT. User has just reached the SMS code screen for a 150,000 KZT transfer.
* **Steps:**
  1. Wait for exactly 121 seconds without performing any action.
  2. Enter the correct SMS code.
  3. Tap Confirm.
* **Expected Result:** System rejects the code. The transfer expires and is cancelled.