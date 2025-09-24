# 🏥 Smart Appointment Booking System

**Smart Appointment Booking System** is an intranet-based hospital application designed to streamline the process of scheduling doctor appointments, managing doctor availability, and tracking patient interactions. Built using **Django**, this role-based system ensures smooth coordination between the **Call Center**, **Counter**, and **Admin** staff.

---

## 📌 Deployment Environment

* **Hosted on:** Hospital Intranet (Internal Network)
* **Backend:** Python (Django Framework)
* **Frontend:** HTML, CSS, JavaScript, Bootstrap
* **Database:** PostgreSQL

---

## 🎯 Project Purpose

This system was developed to digitize and optimize the appointment management process within the hospital, replacing manual tracking systems. It also serves as a centralized tool for managing doctor schedules, patient queries, and appointment confirmations — all while maintaining secure access through role-based user permissions.

---

## 👥 User Roles & Functionalities

### 🧑‍💼 Call Center

* Book appointments for patients
* Add patient-specific **notes** (e.g., urgency, symptoms)
* View **doctor schedules** by department and available slots
* Inform patients about **surgery/test costs** based on department
* Ensure real-time visibility of doctor availability

### 🧾 Counter Staff

* **Confirm appointments** made by the Call Center
* Access and review **notes** written by Call Center staff
* Serve as the final in-person check-in point for patients

### 🔐 Admin

* Create, edit, and delete **doctor profiles** (name, designation, department, qualifications, specialization)
* Set up and manage **doctor slots** and **leave schedules**
* Monitor and manage **user accounts**:

  * Activate/deactivate users (Call Center, Counter, Sub-admins)
  * Edit user access and information
* Ensure synchronization of doctor data across the system

---

## ⚙️ System Features

* 📆 Appointment booking with real-time slot availability
* 👨‍⚕️ Doctor profile & schedule management
* 📋 Patient notes and visit tracking
* 🔒 Secure role-based access control
* 💬 Internal communication via notes between Call Center and Counter
* ❌ Prevention of overbooking or scheduling doctors on leave
* 💲 Display of estimated **procedure and test costs**

---

## 🧪 Testing & QA Documentation

* A full bug testing report is being maintained to document:

  * UI & functional bugs
  * Role-specific behavior issues
  * Slot logic errors
  * Edge case handling
  * etc
* Testing scope includes:

  * Validation (e.g., phone number fields)
  * Slot management behavior
  * Data visibility across roles
  * Appointment integrity during leave conflicts
  * etc

📄 Refer to the `Bug Testing Report` for detailed findings and recommendations.

---

## 👨‍💻 Maintained & Documented By

> **Shafqat Shahriar Arefin**

---

## 🗂️ Status

* ✅ Core functionality complete
* 🔍 Testing and documentation in progress
* 🐞 Bug resolution underway based on QA findings

