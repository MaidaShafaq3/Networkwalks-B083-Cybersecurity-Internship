# 🔐 Milestone 1 — Patient Portal Authentication Bypass

## 🎯 Objective

The objective of Milestone 1 was to identify a vulnerability in the patient portal, gain authenticated access, and retrieve three confidential patient lab reports.

---

## 🔹 1. Patient Portal

The patient portal was identified at:

`https://medirozahospital.com/patient/`

The portal required a username and password to access patient lab reports.

**📸 Screenshot: Patient Portal Login**

> ![Patient Portal Login](<Week-04/Screenshots/1. Patient-Portal-Login.png>)

---

## 🔹 2. SQL Injection Discovery

During testing of the login functionality, a single quote was submitted through the `username` parameter.

The application returned a MySQL `mysqli_query()` syntax error, indicating that the user input was being incorporated into a backend SQL query.

Example:

```text
username='
password=x
```

The response contained:

```text
Warning: mysqli_query(): You have an error in your SQL syntax
```

**📸 Screenshot: SQL Injection Error in Burp Repeater**

> ![SQL Injection Error in Burp Repeater](<Week-04/Screenshots/2. SQL-Injection-Error-in-Burp-Repeater.png>)

---

## 🔹 3. Authentication Bypass

A controlled SQL Injection payload was then used against the username parameter:

```text
username=admin' -- -
password=test
```

The payload modified the SQL query and successfully bypassed the login authentication.

The authenticated session was saved in:

```text
bypass_cookie.txt
```

**📸 Screenshot: Successful SQL Injection Authentication Bypass**

> ![Successful SQL Injection Authentication Bypass](<Week-04/Screenshots/3. Successful-SQL-Injection-Authentication-Bypass.png>)

---

## 🔹 4. Access to Patient Reports

After authentication, the obtained session was reused to access the patient portal and its report download functionality.

Three patient report files were successfully retrieved:

```text
report_1.pdf
report_2.pdf
report_3.pdf
```

The files were saved locally in the Kali Linux Desktop directory.

**📸 Screenshot: Patient Reports Accessible After Login**

> ![Patient Reports Accessible After Login](<Week-04/Screenshots/4. Patient-Reports-Accessible-After-Login.png>)

---

## 🔹 5. Verification of Downloaded Reports

The downloaded files were verified using the `file` command:

```bash
file ~/Desktop/report_1.pdf ~/Desktop/report_2.pdf ~/Desktop/report_3.pdf
```

Output:

```text
report_1.pdf: PDF document, version 1.4, 1 page(s)
report_2.pdf: PDF document, version 1.4, 1 page(s)
report_3.pdf: PDF document, version 1.4, 1 page(s)
```

**📸 Screenshot: Three PDF Files Successfully Retrieved**

> ![Three PDF Files Successfully Retrieved](<Week-04/Screenshots/5. Three-PDF-Files-Successfully-Retrieved.png>)

---

## 📊 Result

Milestone 1 was successfully completed.

The testing demonstrated the following attack chain:

```text
Patient Portal
      ↓
SQL Injection in Login
      ↓
Authentication Bypass
      ↓
Authenticated Patient Session
      ↓
Access to Patient Reports
      ↓
Three Confidential PDF Reports Retrieved
```

### 🔑 Key Finding

The patient portal login functionality was vulnerable to SQL Injection, allowing authentication to be bypassed and restricted patient reports to be accessed.

### 📸 Evidence Collected

* `bypass_cookie.txt` — authenticated session cookie
* `report_1.pdf` — retrieved patient report
* `report_2.pdf` — retrieved patient report
* `report_3.pdf` — retrieved patient report
* Burp Repeater evidence of SQL injection
* Screenshots documenting the authentication bypass and report access

# 👤 Author

**Maida Shafaq**
