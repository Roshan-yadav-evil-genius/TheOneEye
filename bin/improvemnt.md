
## Now: precise questions about the platform (no fluff)

Answer these exactly as they work today. “Not built yet” is an acceptable answer.

### 1. Failure detection (this is critical)

* What counts as a “failure” in your system?

  * Node exception?
  * Timeout?
  * Unexpected output?
  * Business rule violation (e.g., lead not updated)?

Which of these are **automatically detected** vs **manually noticed**?

---

### 2. Notification & response

When something fails:

* Who gets notified? (Slack, email, dashboard, all?)
* Is it instant or batched?
* Can severity be classified (critical vs non-critical)?

This determines whether you’re reactive or operational.

---

### 3. Retry & recovery behavior

If a step fails:

* Does the system retry automatically?
* Is retry logic per-node or per-workflow?
* Is state preserved, or does the workflow restart?

This matters more than most founders realize.

---

### 4. Human intervention point

At what exact moment does a human step in?

* After X retries?
* After time threshold?
* On specific node types only?

And when they step in:

* Can they replay safely?
* Can they patch logic without redeploying everything?

---

### 5. Browser session safety

About the persistent login state:

* Is each client isolated at the filesystem or container level?
* Can one client’s session ever touch another’s?
* How do you revoke access if a client leaves?

This is a trust linchpin.

---

### 6. Change management

When a client changes:

* Their CRM fields
* Their website UI
* Their login credentials
* Their business process

How does TheOneEye detect drift?

* Does anything alert you?
* Or do you discover it only after a failure?

---

### 7. Limits & guardrails

* Do workflows have rate limits?
* Can they runaway or loop infinitely?
* What prevents accidental abuse or blacklisting?

This is especially important with browser automation.

---

### 8. Visibility for the client (or intentional lack of it)

Do clients:

* See dashboards?
* Receive reports?
* Get only outcome updates?

Or is invisibility part of the value?

---

