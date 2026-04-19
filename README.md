# Hospital Management System
### A C++ console application for managing hospital patient records and billing

> Built as a demonstration of core Object-Oriented Programming concepts in C++ — inheritance, operator overloading, exception handling, file I/O, templates, and STL containers.

---

## What It Does

A menu-driven terminal application that simulates the front-desk operations of a hospital. Staff can admit patients, track their stay, manage billing, and discharge them — with all data persisted to a local file between sessions.

---

## Features

- **Admit patients** — auto-assigns the next available bed out of 50, generates a unique patient ID
- **View all patients** — tabular display of currently admitted patients with live bill totals
- **Search by ID** — find any patient and view their full bill breakdown
- **Update records** — modify a patient's diagnosis
- **Billing system** — base charge of ₹3,000/day + additional charges (medicines, tests, etc.)
- **Day increment** — manually advance a patient's stay counter and recalculate bill
- **Bill payment** — full payment required before discharge; change returned if overpaid
- **Discharge** — frees up the bed, marks patient as discharged
- **Persistent storage** — all records saved to `hospital_data.txt` automatically

---

## OOP Concepts Demonstrated

This project was written to cover the following C++ units:

| Concept | Where Used |
|---|---|
| Classes & Objects | `Person`, `Patient`, `Hospital` |
| Inheritance | `Patient` extends `Person` |
| Constructors & Copy Constructor | `Patient(const Patient& p)` |
| Operator Overloading | `operator<<` for `Patient` |
| Exception Handling | `BedNotAvailableException`, `PatientNotFoundException` |
| Templates | `searchPatient<T>()` |
| File I/O | `saveToFile()`, `loadFromFile()` with `|`-delimited format |
| STL Containers | `vector<Patient>` for patient list |
| Arrays | `bool beds[100]` for bed tracking |

---

## Project Structure

```
Hospital-management-system/
├── patient.cpp         # Full source code (365 lines)
├── patient.exe         # Pre-compiled Windows executable
└── hospital_data.txt   # Auto-generated data file (created on first run)
```

---

## How to Run

**Option 1 — Run the pre-compiled executable (Windows)**
```
patient.exe
```

**Option 2 — Compile from source**

Using g++:
```bash
g++ patient.cpp -o patient
./patient        # Linux/Mac
patient.exe      # Windows
```

Using any C++11 or later compiler. No external dependencies.

---

## Menu Options

```
=== Hospital Management System ===
1. Admit Patient
2. View Patients
3. Search Patient
4. Update Patient
5. Add to Bill
6. Increment Days
7. Pay Bill
8. Discharge Patient
9. Exit
```

---

## Billing Logic

```
Total Bill = (Days Admitted × ₹3,000) + Additional Charges

Example:
  3 days stay     = ₹9,000
  Lab test added  = ₹1,500
  Total           = ₹10,500
```

A patient cannot be discharged until their bill is fully paid.

---

## Data File Format

Records are stored in `hospital_data.txt` using a pipe-delimited format:

```
<nextPatientID>
<total_record_count>
<id>|<name>|<age>|<contact>|<disease>|<bed>|<additionalCharges>|<daysAdmitted>|<isAdmitted>
```

The file is read on startup and written after every operation.

---

## Author

**K Karthik Pai** — [@k-karthik-pai](https://github.com/k-karthik-pai)
