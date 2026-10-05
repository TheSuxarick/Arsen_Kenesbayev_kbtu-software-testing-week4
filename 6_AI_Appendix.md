# AI Appendix (Level 1 Policy)

## 1. Prompts Used
I initially used an AI assistant to help structure my raw test design notes from Week 3 into the formal documentation formats required for Week 4. Later, I used a second AI to critically review the first AI's output against the lecture requirements, and then prompted the original AI to implement the valid corrections.

**Prompt example for initial generation:**
> "Here are my test design notes from Week 3 (Equivalence Partitioning, BVA, Decision Tables, State Transitions). Please help me reformat 12 of these checks into runnable test cases."

**Prompt example for Defect Reports:**
> "Help me draft 3 mock defect reports based on the edge cases I identified last week. Use exactly these fields: Title, Environment, Preconditions, Steps to reproduce, Expected result, Actual result, Reproducibility, Severity, Priority, Evidence."

**Prompt example for AI-assisted review and correction:**
> "Here is a critique from another AI regarding your previous output. It points out missing upper BVA boundaries, missing 'Traces to' fields in bugs, and a logical contradiction with the mock defects. Please apply the changes that you agree are correct."

## 2. Raw Output
*The AI initially generated Markdown structures based on my data. For example, for the SMS code defect, the AI provided:*
> **Title:** SMS Confirmation: Transfer executes successfully when correct code is entered after the 120-second expiration.
> **Environment:** iOS 18.2, app 4.11.0 build 2291, test env 2
> ...

## 3. What I Changed and Why
* **AI Peer Review Application:** I actively used a second AI to review the initial draft. Based on this review, I made several critical adjustments to align perfectly with the lecture slides:
  * **BVA Correction:** The initial generation missed the upper boundaries (500,000 and 500,001) for Amount limits. I updated the test cases to ensure proper Boundary Value Analysis for both minimum and maximum boundaries as requested in the assignment.
  * **Traceability in Defects:** I manually added the "Traces to" field in the defect reports, which was initially omitted, to fully comply with the "Anatomy of a defect report" from the lecture.
  * **Defect 3 Redesign:** The AI initially assumed an expected result for a midnight transfer. I corrected this to report a "Requirement Ambiguity," as the original requirement (REQ-3.2) didn't actually specify midnight behavior.
* **Severity and Priority:** I manually adjusted the Severity and Priority levels. For instance, the AI originally suggested "High" severity for the 100,000 KZT boundary bug, but I downgraded it to "Low" since it only causes slight user inconvenience (an extra SMS step) rather than system failure or financial loss.
* **Mock Data Disclosure:** I explicitly added a disclaimer to the defect reports stating they are mock examples. The AI generated realistic-looking evidence (like "5 of 5 attempts"), which I retained for structure, but clarified their mock status to avoid contradicting the fact that I didn't test a real application.