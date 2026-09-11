# Use-Case Flow Specification

## Use Case: Check Out Tool

**Actors:** Community Member (primary), Library Custodian (supporting), System
**Includes:** Verify Member Eligibility, Calculate Deposit

---

### Preconditions
1. The Community Member has an active, registered account in the system.
2. The requested tool is currently marked as **Available** at a depot locker.
3. The Library Custodian (or self-service kiosk) has access to the depot locker's checkout terminal.

### Postconditions
1. The tool's status is updated to **Checked Out**, linked to the member's account.
2. A security deposit hold has been placed on the member's account, calculated based on the tool's category.
3. A due date is recorded based on the tool's configured loan duration limit.
4. The transaction is logged in the member's borrowing history.

---

### Main Success Scenario
1. The Community Member selects an available tool from the inventory (via app or depot kiosk) and initiates checkout.
2. The system verifies the member's eligibility *«include» Verify Member Eligibility*: confirms the member has no overdue tools and no unresolved deposit balances.
3. The system confirms the tool is still physically available at the selected depot locker.
4. The system calculates the required security deposit for the tool's category *«include» Calculate Deposit*.
5. The system places a deposit hold on the member's account and displays the hold amount for confirmation.
6. The member confirms the checkout.
7. The system sets the tool status to Checked Out, assigns a due date based on the loan duration limit for that tool category, and records the transaction.
8. The system displays a checkout confirmation, including the due date and deposit amount held.

---

### Alternate Flow: Member Has an Overdue Tool

**Trigger:** At step 2, the system finds the member currently has one or more overdue tools.

1. The system halts the checkout process and does not proceed to deposit calculation.
2. The system displays a message informing the member which tool(s) are overdue and by how many days.
3. The member is prompted to return the overdue tool(s) before a new checkout can proceed.
4. The use case ends without a new checkout being created (deposit hold and due date from step 4–7 are never generated).

**Postcondition (alternate):** No new checkout occurs; the tool remains marked Available for other members.
