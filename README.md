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
- **Search by ID** — find an admitted patient and view their full bill breakdown
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
| Exception Handling | `BedNotAvailableException`, `std::invalid_argument` (an unused `PatientNotFoundException` is also declared) |
| Templates | `searchPatient<T>()` |
| File I/O | `saveToFile()`, `loadFromFile()` with `|`-delimited format |
| STL Containers | `vector<Patient>` for patient list |
| Arrays | `bool beds[100]` for bed tracking; 50 beds enabled in `main()` |

---

## Project Structure

```text
Hospital-management-system/
├── patient.cpp         # Application source code
├── README.md           # Project documentation
├── LICENSE.txt         # MIT license
└── .gitignore          # Excludes local records and build output
```

`hospital_data.txt` is generated in the working directory when records are saved
or the program exits normally. Executables and local records are not distributed
as source files.

---

## How to Run

Requires a C++11 or later compiler (for example, g++). No external libraries are
needed. Run these commands from the project directory.

**Windows (PowerShell, with g++ installed and on PATH)**

```powershell
g++ -std=c++11 -Wall -Wextra -pedantic patient.cpp -o patient.exe
.\patient.exe
```

**Linux / macOS (with g++ installed)**

```bash
g++ -std=c++11 -Wall -Wextra -pedantic patient.cpp -o patient
./patient
```

Choose **9. Exit** to close the application normally.

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

A patient starts with one billed day. Days advance only through the menu, not automatically with elapsed time. A patient cannot be discharged until their bill is fully paid. Partial payments are rejected; overpayments return change.

Payment clears the balance by setting `additionalCharges` to the negative room charge. This field therefore represents a balance adjustment after payment, not an itemized payment history. Adding charges or incrementing days after payment creates a new balance.

---

## Data File Format

Records are stored in `hospital_data.txt` using a pipe-delimited format:

```
<nextPatientID>
<total_record_count>
<id>|<name>|<age>|<contact>|<disease>|<bed>|<additionalCharges>|<daysAdmitted>|<isAdmitted>
```

The file is read on startup and rewritten after successful changes and on normal
exit. Discharged records remain in the file but do not appear in searches or the
active-patient list. `isAdmitted` is `1` for an active admission and `0` otherwise.

## Scope and Limitations

This is an educational console project, not a production hospital system.

- Use fictional records: storage is plain text with no authentication or encryption.
- Enter valid numeric values when prompted. Non-numeric input is not recovered
  automatically; restart the application if the input stream fails.
- Do not use `|` in text fields or manually edit the data file: the parser assumes
  valid records and does not validate corrupted files or bed numbers.
- Run one instance at a time from a writable directory. Save failures are not
  reported, and concurrent instances can overwrite each other's records.
- Back up `hospital_data.txt` before resetting or moving records. The file path
  is relative to the directory from which the application is launched.

## License

Licensed under the [MIT License](LICENSE.txt).

---

## Author

**K Karthik Pai** — [@k-karthik-pai](https://github.com/k-karthik-pai)
