# Traceability Matrix

| Requirement ID | Requirement Description | Test Cases | Technique Used | Coverage Status |
| :--- | :--- | :--- | :--- | :--- |
| **REQ-3.1** | Amount limits (100 – 500,000 KZT) | TR-AMT-001<br>TR-AMT-002<br>TR-AMT-003<br>TR-AMT-004 | Equivalence Partitioning (EP), Boundary Value Analysis (BVA) | Covered |
| **REQ-3.2** | Daily limit (<= 1,000,000 KZT) | TR-DAY-001<br>TR-DAY-002<br>TR-DAY-003<br>TR-DAY-004 | Decision Table, Boundary Value Analysis (BVA) | Covered |
| **REQ-3.3** | SMS code required for amount > 100,000 KZT | TR-SMS-001<br>TR-SMS-002<br>TR-SMS-003<br>TR-SMS-004 | State Transition | Covered |
| **REQ-3.4** | Insufficient balance handling | — | — | **NOT COVERED** |

## Notes on Uncovered Requirements
**REQ-3.4 (Insufficient balance handling):** This requirement is currently marked as NOT COVERED. During the test design phase, it was identified that the provided specifications do not explicitly define the system's behavior when a user attempts a transfer that exceeds their current account balance. 

Testing for this scenario is blocked pending clarification from the Business Analyst.