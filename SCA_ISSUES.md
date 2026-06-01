# OSS Triage & Remediation Workflow
## Managing New Open-Source Vulnerabilities
---

### Step 1: The Initial Assessment
**When a new vulnerability is detected, the path splits immediately based on one question:**

## *Is a fixed version available from the maintainers?*

---

### Scenario A: A Fix Version IS Available
**If a patch or upgraded version exists, evaluate the integration impact:**

* **Does the upgrade require heavy regression testing?**
  * **NO:** Safe, non-breaking update $\rightarrow$ **Upgrade immediately.**
  * **YES:** High risk of breaking APIs $\rightarrow$ *Proceed to applicability check.*

---

### Verifying Applicability (Fix Available)
**If the upgrade is risky, check if you are actually exposed:**

* **Is the vulnerable code path reachable in your application?**
  * **NO:** Bypasses immediate upgrade $\rightarrow$ **Move to End / Postpone.**
  * **YES:** You are actively exposed $\rightarrow *Check for mitigations.*

---

### Evaluating Mitigations (Fix Available)
**If you are exposed and the upgrade requires heavy testing:**

* **Can the vulnerability be mitigated via config or workarounds?**
  * **NO:** Forced to accept the testing overhead $\rightarrow$ **Upgrade.**
  * **YES:** Apply the temporary fix to buy time $\rightarrow$ **Mitigate.**

---

### Scenario B: NO Fix Version Available
**When maintainers haven't released a fix, ask right away:**

## *Is the vulnerability applicable to our app?*

* **NO:** The vulnerable feature isn't used $\rightarrow$ **End (No action required).**
* **YES:** Proceed down the cascading line of alternative remediation steps.

---

### Cascading Options (No Fix Available)

1. **Can it be Mitigated?**
   * Apply a configuration change, firewall rule, or environment adjustment.
2. **Can it be Patched?**
   * Manually write a hotfix or cherry-pick a commit directly to the source code.
3. **Can it be Removed?**
   * Completely swap out or delete the package from the application.

---

### The Last Resort: Risk Acceptance

If **no fix** exists, the flaw is **applicable**, it **cannot be mitigated or patched**, and the package is **too vital to remove**:

* **Action:** **Accept Risk**
* Document the flaw, flag the security debt, and monitor for future vendor updates.
