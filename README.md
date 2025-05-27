 Smart_Appointment_System Bug testing

# Appointment System – Bug Testing Report

This document presents a structured and well-documented list of issues discovered during functional and UI testing of the Appointment System. All findings are categorized and explained for better clarity, including screenshots for reference.

---

## 🔐 User: Admin

### 📋 Appointment Module

#### 🐞 Bug 1: Phone Field Validation

* **Location:** `All Doctor List > Edit` and `Create Doctor`
* **Issue:** The phone number field accepts alphabets and special characters.
* **Expected:** Only numeric input should be accepted.

#### 🐞 Bug 2: Slot Booking – No Clear/Delete Option

* **Issue:** No button available to clear the slot list.
* **Impact:** Admin must manually remove slots one by one.

#### 🐞 Bug 3: Doctor Schedule Visibility Discrepancy

* **Description:** Admin sets a schedule for a doctor on Friday, but Call Center user cannot see it.
* **Impact:** Appointments cannot be booked for that doctor on Friday.

#### 🐞 Bug 4: Minor – No Phone Field Regulation

* **Description:** Inconsistent validation when inputting phone numbers.

#### 🐞 Bug 5: View Appointments Link Not Working

* **Location:** Admin dashboard
* **Issue:** Clicking the link results in no action.

#### 🐞 Major Bug: Doctor Leave & Slot Logic

* **Symptoms:**

  * Doctor on leave can still be assigned to appointments.
  * When slots are full, patients can still be added.
  * Patients whose appointments were scheduled for 9:00 AM and arrived at 2:00 PM disappeared after the doctor went on leave at 1:00 PM.
* **Assumption:** System wrongly marks them as completed.
* **Impact:** Critical patient data loss from "All Patients List".

---

## 🧑‍💼 User: Call Center

### 📅 Appointment Module

#### 🐞 Bug 6: Autofill Not Working for Doctor Details

* **Issue:** When an appointment is booked, the selected doctor's name and department are not autofilled.
* **Expected:** Fields should prepopulate based on the selection.

#### 🐞 Bug 7: Search Not Recognizing Alternative Phone Numbers

* **Issue:** Patients' alternate numbers cannot be used in the search bar.

---

## 📸 Screenshots

> Screenshots are referenced inline above. Make sure all image links render correctly on GitHub/GitLab.

---

## ✅ Recommendations

* Enforce input validation for phone number fields using regex or input masks.
* Implement a "Clear All" button in Slot Booking.
* Synchronize doctor schedules between Admin and Call Center views.
* Disallow appointment creation for doctors on leave or fully booked.
* Log and handle patient reschedules with timestamp-based verification.
* Ensure search functionality indexes both primary and alternate numbers.

---

## 📌 Notes

* Major bugs should be prioritized for immediate patching.
* A regression test suite is advised post-resolution of each high-severity issue.
* Coordinate with backend and frontend teams to confirm root causes and fix rollout.

---

*Last updated after field test on: **May 26, 2025 @ 4:10 PM***
