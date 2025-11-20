🏥 Full-Stack Queue Management System — Django Specification
🧩 Overview

You are to develop a Full-Stack Queue Management System using Django (backend) and HTML/CSS/JS or a frontend framework (React) for the interface.
The system manages patients through multiple departments, from registration → optometrist → doctor.

👥 User Roles and Access
1. Super Admin

Default Django superuser.

Can add/delete any of the 3 user types:

Counter

Admin

Patient Care

2. Counter

Has a dashboard to register new and old patients.

Enters all patient information into the system.

3. Admin

Assigns:

Rooms for doctors and optometrists.

Schedules (days, slots) for each doctor.

Department allocations (which doctor/optometrist belongs to which department).

Patient Care users to departments.

4. Patient Care

Manages queue operations for two sections:

Optometrist Section

Doctor Section

Controls patient flow:

Waiting → Calling → Processing

Handles emergency cases and room reassignment (e.g., if a doctor leaves for surgery).

🏢 Departments

Each department has two sections (Optometrist and Doctor) and 5 rooms per section:

Department Optometrist Rooms Doctor Rooms
Cataract A1–A5 B1–B5
Retina A1–A5 B1–B5
Glaucoma A1–A5 B1–B5
Cornea A1–A5 B1–B5
Private A1–A5 B1–B5
General A1–A5 B1–B5

There are 60 doctors and 30 optometrists total.
Names should be Bangladeshi-based, and the system time is set to 2025.

🧾 Counter (Patient Registration)

The Counter user enters the following details:

Field Type / Description
Name Text
Age Number
Care Of Name Text
Address Text
Phone No Text
MRN No Auto-generated or manually entered
Department Dropdown (Cataract, Retina, Glaucoma, Cornea, Private, General)
Gender Male / Female / Other
Emergency Boolean (Yes/No)
Specific Doctor Dropdown (filtered by Department) or left blank for Patient Care to assign

All patient data is stored in the database.

🧑‍💼 Admin Functions

Admins can:

Configure which doctor/optometrist works in which department.

Assign days and slots per day for each doctor.

Link Patient Care staff to specific departments.

Define available rooms and capacity for each department.

👩‍⚕️ Patient Care — Queue Management

Each department has two active queues:

optometryQueue

doctorsQueue

Each queue has three patient states:

calling – Patient currently being called into a room.

processing – Patient currently being examined.

waiting – Patients waiting in line.

Example data structure:

{
"name": "Rahim Uddin",
"room": "A1",
"mrn": "OPT-2025-001",
"age": 42,
"gender": "Male",
"emergency": false
}

⚙️ System Components (Front-End Logic)
1. Data Setup
const optometryQueue = {...};
const doctorsQueue = {...};


Contains mock or live queue data for each department.

2. Room Configuration
const optometryRooms = ['A1', 'A2', 'A3', 'A4', 'A5'];
const doctorsRooms = ['B1', 'B2', 'B3', 'B4', 'B5'];


Tracks rooms in use and their rotation order.

3. Utility Functions
Function Description
updateDateTime() Displays real-time clock.
showSuccessMessage() Displays temporary success alerts.
updatePatientCount() Shows number of patients in all states.
updateTimestamp() Shows last data refresh time.
4. Rendering Functions
Function Description
renderCallingCard() Displays the patient being called. Highlights emergency cases.
renderProcessingGrid() Shows room occupancy grid.
renderWaitingPatients() Displays waiting list and MRN “chips” for quick actions.
5. Patient Interaction
Function Purpose
handleMrnChipClick() Opens detailed patient info popup.
populateRoomDropdown() Loads available room options.
closePatientCard() Closes patient info overlay.
6. Queue Logic

Core automation for moving patients through queues:

Function Description
findNextPatientForRoom(queue, room) Finds next eligible patient (emergencies prioritized).
getAvailableRooms(queue, rooms) Returns list of free rooms.
assignRoomToPatient(queue, rooms) Assigns waiting patients to available rooms.
simulateQueueUpdates() Moves patients through stages every few seconds.
7. Emergency Handling

When a patient is marked as emergency:

They move to the front of the queue.

If a doctor is unavailable, Patient Care can reassign rooms or select a substitute doctor.

8. Initialization
function init() {
updateDateTime();
renderQueueSection(optometryQueue, 'optometry', optometryRooms, 'optometryTimestamp');
renderQueueSection(doctorsQueue, 'doctors', doctorsRooms, 'doctorsTimestamp');
setInterval(updateDateTime, 1000);
setInterval(simulateQueueUpdates, 8000);
}
init();

💻 User Interface Expectations

Top header: Current date & time.

Two panels: Optometrist and Doctor queues.

Each panel shows:

Calling card (current patient)

Room grid (processing)

Waiting list + MRN chips

MRN chip click → Patient detail popup

Mark as Emergency button → reorders queue

📋 Summary Table
Component Purpose
Data Structures Hold queue and patient info per department
Rendering Functions Build and update visual UI
Event Handlers Manage interactions
Queue Logic Advance patient flow
Initialization Start simulation and clock updates
🕰️ Notes

Each department: 5 Optometrist Rooms + 5 Doctor Rooms

Total: 6 Departments → 60 Doctors + 30 Optometrists

All names should be Bangladeshi-based (e.g., Rahim, Karim, Nasrin, Ayesha).

Time & data context: Year 2025


🧑‍💼 Admin Section

The Admin section manages the organizational setup of the queue management system — assigning doctors, optometrists, and patient care users to departments, rooms, and schedules.
It acts as the configuration control panel for the entire application.

🧠 Overview

The Admin dashboard has three main configuration panels:

Doctor & Optometrist Management

Add, edit, or remove doctors/optometrists.

Assign them to specific departments.

Assign working days and time slots.

Assign rooms (A1–A5 or B1–B5).

Department Setup

Configure each of the six departments:

Cataract

Retina

Glaucoma

Cornea

Private

General

Assign optometrist rooms (A1–A5) and doctor rooms (B1–B5).

Manage capacity per room.

Patient Care Assignment

Assign which Patient Care user handles which department.

Reassign easily when staff changes.

All updates should dynamically update the system configuration database.

🧩 Major Sections of the Script
1. Data Setup

Example dataset structure for Admin panel:

const departments = ['Cataract', 'Retina', 'Glaucoma', 'Cornea', 'Private', 'General'];

const doctors = [
{ id: 1, name: "Dr. Rahim Hossain", department: "Retina", room: "B2", days: ["Sun", "Tue"], slotsPerDay: 10 },
{ id: 2, name: "Dr. Nasrin Akter", department: "Cataract", room: "B3", days: ["Mon", "Wed"], slotsPerDay: 8 }
];

const optometrists = [
{ id: 1, name: "Shahidul Islam", department: "Retina", room: "A1", days: ["Sun", "Tue"], slotsPerDay: 15 },
{ id: 2, name: "Ayesha Begum", department: "Cornea", room: "A2", days: ["Thu"], slotsPerDay: 10 }
];

const patientCareAssignments = [
{ id: 1, user: "Fatema Khatun", department: "Glaucoma" },
{ id: 2, user: "Kamrul Hasan", department: "General" }
];

2. Room Configuration

Each department has fixed room identifiers:

const optometristRooms = ['A1', 'A2', 'A3', 'A4', 'A5'];
const doctorRooms = ['B1', 'B2', 'B3', 'B4', 'B5'];


Admins can assign which user (doctor/optometrist) occupies which room per department.
The system validates no room conflicts — e.g., two doctors cannot share B3 at the same time.

3. DOM References
const addDoctorBtn = document.getElementById('addDoctorBtn');
const addOptometristBtn = document.getElementById('addOptometristBtn');
const departmentSelect = document.getElementById('departmentSelect');
const roomSelect = document.getElementById('roomSelect');
const scheduleTable = document.getElementById('scheduleTable');
const patientCareAssignForm = document.getElementById('patientCareAssignForm');


These elements connect the UI to functions for adding new users, assigning rooms, or viewing schedules.

4. Utility Functions
Function Description
showSuccessMessage() Displays success alert when assignments are saved.
clearForm() Resets input fields after submission.
validateRoomAvailability(room, department, role) Ensures room is not already assigned to another doctor/optometrist.
updateTimestamp() Updates last saved/modified timestamp for any change.
5. Rendering Functions
Function Description
renderDoctorTable() Displays list of all doctors, their departments, rooms, and schedules.
renderOptometristTable() Displays all optometrists with similar info.
renderDepartmentSetup() Lists each department with its current room mappings and assigned staff.
renderPatientCareAssignments() Shows which patient care users are assigned to which department, with option to reassign.

Each table includes:

Edit button ✏️ → Opens form for quick modification.

Delete button 🗑️ → Removes user/assignment.

6. Form Interaction & Event Handlers
Event Description
addDoctorBtn.addEventListener('click', openAddDoctorForm) Opens modal to add a new doctor.
addOptometristBtn.addEventListener('click', openAddOptometristForm) Opens modal to add a new optometrist.
patientCareAssignForm.addEventListener('submit', savePatientCareAssignment) Saves patient care–to–department assignment.
roomSelect.addEventListener('change', validateRoomAvailability) Validates room selection instantly.

When a doctor or optometrist is added:

Their department, room, and schedule are saved.

A success popup appears.

All tables refresh to show the updated configuration.

7. Scheduling Logic

Core scheduling automation and validation:

Function Description
assignSchedule(userId, days, slotsPerDay) Saves daily schedules for each doctor/optometrist.
getAvailableDays(department) Returns days where there’s capacity.
checkSlotConflict(department, day, room) Prevents overlapping slots in the same room.

Example:
If Dr. Rahim is assigned to B1 (Retina) on Sunday, no other Retina doctor can occupy B1 on that day.

8. Data Persistence (Backend)

Each admin action triggers a Django backend API call:

Endpoint Method Purpose
/api/admin/add_doctor/ POST Add new doctor record
/api/admin/add_optometrist/ POST Add new optometrist record
/api/admin/assign_room/ POST Assign room and department
/api/admin/assign_patient_care/ POST Link patient care user to department
/api/admin/update_schedule/ PUT Update working days and slots
/api/admin/delete_user/<id>/ DELETE Remove user

All data is validated on both frontend and backend.

9. Initialization
function initAdminDashboard() {
renderDoctorTable();
renderOptometristTable();
renderDepartmentSetup();
renderPatientCareAssignments();
updateTimestamp();
}
initAdminDashboard();


On page load:

Fetches all existing configurations from the backend.

Renders department tables.

Starts listening for changes in forms and selects.

🖼️ What the Admin Sees

The Admin dashboard visually contains:

🔧 Tabs or Cards:

“Doctors”

“Optometrists”

“Departments”

“Patient Care Assignments”

📅 Schedule View: Calendar-style view for doctor availability.

🧾 Room Assignment Tables: Clear mapping of A/B rooms per department.

✅ Save / Update / Delete actions with confirmation popups.

⏰ Last Updated timestamp footer.

🧭 In Summary
Component Purpose
Data Structures Store and organize doctor, optometrist, and assignment data
Rendering Functions Build interactive tables and dashboards
Event Handlers Handle user input and CRUD operations
Scheduling Logic Manage working days and slot validation
API Integration Save configurations to backend
Initialization Loads dashboard and binds all UI controls
⚙️ Notes

Each department: 5 Optometrist rooms (A1–A5) + 5 Doctor rooms (B1–B5)

Total staff: 60 doctors, 30 optometrists, 6 patient care users

All names and data localized for Bangladesh (year 2025)

Time zone should match Asia/Dhaka


💁‍♂️ Counter Section

The Counter Section is the first point of patient interaction.
Counter users register new patients, enter demographic details, assign a department for checkup, and (optionally) refer them to a specific doctor.
All patient data entered here flows into the queue management system, where Patient Care users manage the next stages.

🧠 Overview

The Counter Dashboard consists of the following areas:

New Patient Registration Form

Collects all patient demographic and visit details.

Patient List / Recent Registrations

Displays the last few patients registered (with search and filter).

Emergency Flagging

Allows marking a patient as an emergency case.

Department & Doctor Selection

Dropdown filters for assigning departments and, optionally, specific doctors.

MRN (Medical Record Number) Generator

Automatically creates unique patient MRNs (e.g., MRN-2025-0001).

All entries are validated and stored in the backend database.

🧩 Major Sections of the Script
1. Data Setup

Example of initial data representation:

const departments = ['Cataract', 'Retina', 'Glaucoma', 'Cornea', 'Private', 'General'];

const patientList = [
{
id: 1,
name: "Rahim Uddin",
age: 42,
careOf: "Karim Uddin",
address: "Dhanmondi, Dhaka",
phone: "01712345678",
mrn: "MRN-2025-001",
department: "Retina",
gender: "Male",
emergency: false,
doctor: "Dr. Nasrin Akter",
createdAt: "2025-01-10 10:45 AM"
}
];


All patients entered here are stored in the backend (Django model: Patient).

2. DOM References
const addPatientForm = document.getElementById('addPatientForm');
const departmentSelect = document.getElementById('departmentSelect');
const doctorSelect = document.getElementById('doctorSelect');
const emergencyCheckbox = document.getElementById('emergencyCheckbox');
const patientTable = document.getElementById('patientTable');
const successPopup = document.getElementById('successPopup');


These connect the form and the patient table to the frontend logic.

3. Utility Functions
Function Description
generateMRN() Auto-generates a new MRN based on date and incremental ID (MRN-2025-001).
showSuccessMessage() Displays confirmation popup after successful patient entry.
clearForm() Resets the form after submission.
filterDoctorsByDepartment(dept) Dynamically loads doctors belonging to the selected department.
validateFormInputs() Ensures required fields (name, phone, department, gender) are filled.
4. Rendering Functions
Function Description
renderPatientTable() Displays all registered patients in a table format.
renderDoctorDropdown() Populates the doctor dropdown based on department.
renderDepartmentDropdown() Shows all departments for selection.

The patient table includes:

Patient Name

MRN

Department

Doctor (if assigned)

Emergency status

Registration time

5. Form Interaction
Event Description
departmentSelect.addEventListener('change', handleDepartmentChange) Loads available doctors when department changes.
addPatientForm.addEventListener('submit', handlePatientSubmit) Saves new patient entry.
emergencyCheckbox.addEventListener('change', handleEmergencyMarking) Highlights emergency patient in form UI.

Example logic:

function handlePatientSubmit(event) {
event.preventDefault();
const formData = new FormData(addPatientForm);
const newPatient = {
name: formData.get('name'),
age: formData.get('age'),
careOf: formData.get('careOf'),
address: formData.get('address'),
phone: formData.get('phone'),
mrn: generateMRN(),
department: formData.get('department'),
gender: formData.get('gender'),
emergency: formData.get('emergency') === 'on',
doctor: formData.get('doctor') || null,
createdAt: new Date().toLocaleString()
};
patientList.push(newPatient);
renderPatientTable();
showSuccessMessage();
clearForm();
}

6. MRN Generation Logic

The MRN is unique for each patient and follows a standard pattern:

MRN-[YEAR]-[SEQUENCE]


Example:

MRN-2025-0001
MRN-2025-0002


Implementation:

function generateMRN() {
const nextId = patientList.length + 1;
return `MRN-${new Date().getFullYear()}-${String(nextId).padStart(4, '0')}`;
}

7. Backend Integration (Django API)

Each patient record is stored in the Django backend using REST API endpoints.

Endpoint Method Purpose
/api/counter/add_patient/ POST Add new patient record
/api/counter/get_patients/ GET Fetch recent patients
/api/counter/get_doctors/<department>/ GET Fetch doctors for department
/api/counter/delete_patient/<id>/ DELETE Remove patient (if needed)

Django Models (simplified):

class Patient(models.Model):
name = models.CharField(max_length=100)
age = models.IntegerField()
care_of = models.CharField(max_length=100)
address = models.TextField()
phone = models.CharField(max_length=15)
mrn = models.CharField(max_length=20, unique=True)
department = models.CharField(max_length=50)
gender = models.CharField(max_length=10)
emergency = models.BooleanField(default=False)
doctor = models.ForeignKey(Doctor, null=True, blank=True, on_delete=models.SET_NULL)
created_at = models.DateTimeField(auto_now_add=True)

8. Data Validation Rules

Before saving a patient:

Rule Condition
Phone number Must be 11 digits, start with “01”
Age Must be between 0 and 120
Department Required
Gender Required
MRN Must be unique
Emergency Optional boolean
Doctor Optional; shown only if department has doctors listed

Invalid inputs show inline red warnings and disable the “Submit” button.

9. Initialization
function initCounterDashboard() {
renderDepartmentDropdown();
renderDoctorDropdown();
renderPatientTable();
setInterval(updateDateTime, 1000);
}
initCounterDashboard();


On page load:

Departments and doctor lists populate.

The real-time clock updates.

Patient table refreshes automatically every few seconds.

🖼️ What the Counter User Sees

The Counter Dashboard contains:

🧾 Registration Form

Name, Age, Address, Gender

Department (dropdown)

Doctor (auto-filtered by department)

Emergency checkbox

🩺 MRN Auto Generator (shows MRN preview before submit)

📋 Recent Registrations Table

Displays the last 10 registered patients

✅ Success Popup after adding patient

🔍 Search Bar to find patients by MRN or name

🧭 In Summary
Component Purpose
Data Structures Store and manage patient information
Rendering Functions Build the registration form and patient table
Event Handlers Handle form inputs and submission
MRN Logic Generate unique patient identifiers
Validation Ensure correct input before saving
Backend Integration Persist data to Django models
Initialization Bootstraps the Counter dashboard
⚙️ Notes

Counter users only enter patient data — they cannot modify doctor schedules or queue status.

Every successfully added patient appears in the Patient Care dashboard queues automatically (filtered by department).

Emergency cases are flagged 🔴 and prioritized automatically in the queue system.

Time and date context → Bangladesh, 2025.
