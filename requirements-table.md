# Requirements Table — Community Tool & Equipment Library (PS#52)

**Stakeholders / Actors:** Community Member, Library Custodian

## Functional Requirements

### FR-001 [Priority: High]
**Description:** The system shall calculate required security deposits based on tool category, enforce loan duration limits, and calculate late return fees.
**Acceptance Criteria:**
- Pass: Tool reservation confirmed with deposit hold applied.
- Fail: Member with overdue tools is able to borrow additional high-value equipment.
**Rationale:** Deposits and loan limits protect community assets from loss or extended unavailability, and late fees discourage overdue returns.

### FR-002 [Priority: High]
**Description:** The system shall allow a verified Community Member to reserve and check out an available tool, blocking checkout if the member has any overdue items outstanding.
**Acceptance Criteria:**
- Pass: Checkout succeeds only when the member has zero overdue items and the tool is marked available.
- Fail: A member with an overdue tool successfully checks out a new item.
**Rationale:** Prevents a small number of members from monopolizing shared inventory and enforces accountability before further borrowing.

### FR-003 [Priority: Medium]
**Description:** The system shall allow members to search the tool inventory by category, keyword, or depot locker location, and display current availability status for each matching item.
**Acceptance Criteria:**
- Pass: Search returns only items physically present and unreserved at the selected depot locker.
- Fail: Search shows a tool as available when it is currently checked out.
**Rationale:** Members need accurate, location-aware visibility into inventory to plan pickups across a distributed set of neighborhood lockers.

### FR-004 [Priority: High]
**Description:** The system shall allow a Library Custodian to log a damage assessment at the time of tool return, and automatically calculate any deduction from the member's held deposit based on assessed severity.
**Acceptance Criteria:**
- Pass: A logged "moderate damage" assessment triggers a partial deposit deduction matching the configured damage-tier rate.
- Fail: Damage is logged but the member's deposit record is not updated.
**Rationale:** Ties physical condition checks directly to financial accountability, protecting the shared equipment pool.

### FR-005 [Priority: Medium]
**Description:** The system shall automatically calculate and apply late return fees when a tool is returned after its due date, and update the member's borrowing record accordingly.
**Acceptance Criteria:**
- Pass: A tool returned 3 days late generates a fee matching the configured daily late-fee rate × 3.
- Fail: A late return is processed with no fee applied to the member's account.
**Rationale:** Automating fee calculation removes custodian error and ensures consistent enforcement of return policies.

## Non-Functional Requirements

### NFR-001 [Type: Performance & Security]
**Description:** The tool inventory search must display real-time physical availability across neighborhood depot lockers.
**Priority:** High
**Acceptance Criteria:**
- Pass: Benchmarking tests confirm target latency (e.g. under 2s response) and security standards under simulated peak load.
- Fail: Search results lag behind actual locker inventory by more than the defined staleness threshold.
**Rationale:** Members act on availability data immediately; stale or slow results lead to wasted trips to a locker that turns out to be empty.

### NFR-002 [Type: Reliability & Usability]
**Description:** The system shall remain available and usable during standard library operating hours (e.g. 99.5% uptime), including graceful degradation to cached inventory data if a depot locker's connectivity is temporarily lost.
**Priority:** Medium
**Acceptance Criteria:**
- Pass: During a simulated locker connectivity outage, the system continues to serve last-known inventory status with a "last updated" timestamp rather than failing outright.
- Fail: A single locker's connectivity loss causes the entire system to become unavailable to all members.
**Rationale:** A volunteer-run community system can't guarantee perfect infrastructure at every locker; the system should stay usable even when parts of it are degraded.
