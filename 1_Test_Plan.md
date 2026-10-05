# Test Plan Section: Money Transfer Feature

## 1. Scope
**In Scope:**
* Functional testing of the internal money transfer feature.
* Validation of single transfer amount limits (100 KZT – 500,000 KZT).
* Validation of the daily transfer limit (up to 1,000,000 KZT).
* SMS code confirmation flow and state transitions (for transfers > 100,000 KZT).
* Timeout and retry mechanisms for SMS codes (120-second expiration, 3 wrong attempts).

**Out of Scope:**
* Performance and load testing under high transaction volumes.
* Security and penetration testing.
* Database integrity and backend API direct testing.
* Cross-currency transfers or transfers to other banks.

## 2. Approach
* **Level:** System Testing.
* **Type:** Functional Testing (Black-box).
* **Techniques:** Equivalence Partitioning (EP), Boundary Value Analysis (BVA), Decision Tables, and State Transition Testing.
* **Automation Approach:** Fully manual testing for this release, heavily relying on predefined test cases and checklists for the SMS flow. Exploratory testing will be used around edge cases (e.g., midnight boundary).

## 3. Entry and Exit Criteria
**Entry Criteria:**
* The build is successfully deployed to the test environment.
* Smoke tests pass (the application launches, and the main transfer screen is accessible).
* Test data is prepared and loaded (e.g., test customers with specific balances like 1,000,000 KZT and pre-set daily totals are available).
* Acceptance criteria and requirements are explicitly defined and available to the QA team.

**Exit Criteria:**
* 100% of the 12 selected/planned functional test cases are executed.
* No open Critical or High severity defects remain (or any remaining high defects are formally accepted by the Product Owner in writing).
* Requirements coverage is verified via the Traceability Matrix.
* The residual risks are documented and accepted by the business.

## 4. Top Three Product Risks
1. **Financial Loss via Double Debiting:** A race condition where a user repeatedly taps "Confirm" during a slow network response, causing the system to debit the amount multiple times for a single SMS confirmation.
2. **Security Breach via Expired Codes:** The system incorrectly accepts an expired SMS code (entered after the 120-second window), leading to the execution of a transfer that should have been cancelled.
3. **Daily Limit Bypass at Midnight:** Incorrect daily total calculation for transfers spanning across midnight (e.g., initiated at 23:59, confirmed at 00:01), allowing a user to bypass the 1,000,000 KZT daily limit due to timezone or timestamp handling errors.