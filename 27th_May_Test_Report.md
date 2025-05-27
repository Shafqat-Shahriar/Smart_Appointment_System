# Test on progress

---

## 🐞 Bug: Edit Button Not Working on Page 2 of All Doctor List

* **Location:** `All Doctor List > Page 2`
* **Issue:** The "Edit" button does not respond or load the edit modal/page for doctors listed on the second page.
* **Expected Behavior:** Clicking "Edit" should allow modifying doctor details regardless of pagination.

---

## 🐞 Bug: Manual Slot Entry Conflicts with Auto Generate

* **Scenario:** Manually add a slot (e.g., `10:00 AM to 10:15 AM`) and then click **Auto Generate 15 Minute Slots**.
* **Issue:** Auto-generated slots **start from 9:00 AM**, overriding the manual slot instead of appending or adjusting.
* **Expected Behavior:** Auto-generated slots should consider existing manual entries and **start after the last defined time**.

---

## 🐞 Bug: Doctor Code Reuse Issue

* **Scenario:**
  - Create a doctor with code: `"abcd"`
  - Delete this doctor.
  - Try to create another doctor with the same code `"abcd"`
* **Issue:** The system **throws an error or fails silently**, not allowing reuse of the same doctor code.
* **Expected Behavior:** After deletion, the system should **free up the doctor code** for reuse or at least **provide a clear message** that it's reserved.

---
