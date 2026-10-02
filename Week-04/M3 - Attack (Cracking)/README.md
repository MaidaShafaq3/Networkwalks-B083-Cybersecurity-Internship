# 🔐 M3 – Critical Data Exposure

## 🎯 Objective

The objective of this milestone was to identify a critical data exposure on the client server and determine whether confidential hospital employee and shareholder information was publicly accessible.

### 📋 Tasks

* Find the salaries of all hospital employees.
* Find the shareholder details of the hospital.

Written permission for testing was granted.

---

## 🔹 1. Identifying the Exposed Resource

During the previous reconnaissance phase, the server's `robots.txt` file referenced an `/old/` directory.

The directory was accessible without authentication and exposed a directory listing containing an SQL database backup:

```text
/old/mediroza_db_backup_2019.sql
```

The backup was accessible directly from the web server.

### 📸 Evidence

> ![Exposed Backup Directory](<../Screenshots/12. Exposed Backup Directory.png>)

---

## 🔹 2. Retrieving the Database Backup

The exposed SQL backup was downloaded for analysis:

```bash
curl -O https://medirozahospital.com/old/mediroza_db_backup_2019.sql
```

The file was then inspected locally.

```bash
file mediroza_db_backup_2019.sql
wc -l mediroza_db_backup_2019.sql
```

The file was identified as an ASCII SQL dump containing 93 lines.

The HTTP response also confirmed that the file was directly accessible:

```text
HTTP/1.1 200 OK
Content-Type: text/x-sql
```

### 📸 Evidence

> ![Database Backup Retrieved](<../Screenshots/13. Database Backup Retrieved.png>)

---

## 🔹 3. Database Metadata Analysis

The beginning of the SQL dump contained metadata identifying the database as an internal HR database.

The backup indicated:

* Database: `mediroza_hr`
* CMS: Mediroza CMS 1.4.2
* Backup date: 2019-08-27
* Backup timestamp: 02:14:03

The backup also contained a warning indicating that it included confidential staff and shareholder records.

This demonstrated that a sensitive internal database backup had been placed inside a publicly accessible web directory.

### 📸 Evidence

> ![Database Metadata](<../Screenshots/14. Database Metadata.png>)

---

## 🔹 4. Database Structure

The SQL dump was analysed to identify the tables and fields contained within the backup.

The database contained two relevant tables:

```text
staff
shareholders
```

### Staff Table

The `staff` table contained the following fields:

| Field                | Description                             |
| -------------------- | --------------------------------------- |
| `id`                 | Employee record ID                      |
| `full_name`          | Employee name                           |
| `job_title`          | Employee job title                      |
| `department`         | Employee department                     |
| `email`              | Employee email address                  |
| `phone`              | Employee phone number                   |
| `national_id`        | Employee national identification number |
| `monthly_salary_zar` | Employee monthly salary                 |
| `date_joined`        | Employment start date                   |

The presence of `monthly_salary_zar` directly exposed employee salary information.

### Shareholders Table

The `shareholders` table contained:

| Field              | Description           |
| ------------------ | --------------------- |
| `id`               | Shareholder record ID |
| `shareholder_name` | Shareholder name      |
| `share_percent`    | Percentage ownership  |
| `shares_held`      | Number of shares      |
| `share_class`      | Share classification  |

This exposed shareholder ownership information, including the percentage and number of shares held.

---

## 🔹 5. Employee Salary Exposure

The `staff` table was analysed for the employee salary information.

The following field was particularly sensitive:

```text
monthly_salary_zar
```

The database therefore exposed employee compensation information together with identifying information such as names, departments, contact details and national IDs.

### 📸 Evidence

> ![Employee Salary Data](<../Screenshots/15. Employee Salary Data.png>)

> **Privacy note:** Actual employee names, national IDs, contact information and salary values have been redacted from the GitHub evidence.

---

## 🔹 6. Shareholder Information Exposure

The `shareholders` table was analysed to identify the ownership information exposed by the backup.

The exposed records contained:

* Shareholder names
* Percentage ownership
* Number of shares held
* Share class

### 📸 Evidence

> ![Shareholder Data](<../Screenshots/16. Shareholder Data.png>)

> **Privacy note:** Actual shareholder records and ownership values have been redacted from the public repository.

---

## 🔹 7. Why This Is a Critical Exposure

The issue was not simply the presence of an old file.

The server allowed an unauthenticated external user to:

1. Discover the `/old/` directory.
2. View its contents.
3. Identify the database backup.
4. Download the SQL file directly.
5. Read the database structure.
6. Access confidential employee information.
7. Access employee salary information.
8. Access shareholder ownership information.

No application authentication was required to obtain the database backup.

### 🚨 Exposure Chain

```text
Public Web Server
       │
       ▼
/old/
       │
       ▼
Directory Listing
       │
       ▼
mediroza_db_backup_2019.sql
       │
       ▼
Internal HR Database
       │
       ├── staff
       │     ├── Employee details
       │     ├── Contact information
       │     ├── National IDs
       │     └── Monthly salaries
       │
       └── shareholders
             ├── Shareholder names
             ├── Ownership percentage
             ├── Shares held
             └── Share class
```

---

## 🔹 8. Findings Summary

| Finding                             | Result    |
| ----------------------------------- | --------- |
| Public `/old/` directory            | Confirmed |
| SQL database backup exposed         | Confirmed |
| Authentication required             | No        |
| Employee records exposed            | Confirmed |
| Employee salary information exposed | Confirmed |
| National ID information exposed     | Confirmed |
| Shareholder information exposed     | Confirmed |
| Ownership percentages exposed       | Confirmed |

---

## 📊 Result

A publicly accessible database backup was discovered on the client server.

The backup contained sensitive information from the hospital's internal HR database, including:

* Employee names and employment information
* Employee contact information
* National identification numbers
* Employee monthly salaries
* Shareholder names
* Share ownership percentages
* Number of shares held
* Share classes

The exposure was possible because the database backup was stored inside a publicly accessible web directory.

### 🔧 Recommended Remediation

The exposed backup should be removed from the public web directory and stored outside the web root.

Additional recommended controls include:

* Disable directory listing.
* Remove old and unused files from production servers.
* Prevent database backups from being stored inside publicly accessible directories.
* Review the server for other exposed backups and configuration files.
* Restrict access to sensitive HR and corporate information.
* Implement regular web-server content and backup audits.

> **Security Note:** The original SQL backup and extracted confidential records should not be committed to the public GitHub repository. Evidence screenshots should redact employee names, national IDs, contact information, salary values and shareholder information.


👤 Author

Maida Shafaq
