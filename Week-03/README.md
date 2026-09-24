# 🔐 Week 3 – Password Cracking with JTR & NetworkWalks Tools

**Cybersecurity & Ethical Hacking Internship – NetworkWalks**

## 📌 Overview

This project covers the Week 3 practical tasks related to password cracking and password security.

The practical work was divided into two modules:

- **W3-PM1:** Password Cracking using John the Ripper (JTR) and Johnny
- **W3-PM2:** Password Cracking using NetworkWalks Tools

All tests were performed in a controlled lab environment using training PDFs and PDFs created for testing purposes.

The main goal was to understand how password-protected files can be tested using password-cracking tools and to understand the importance of using strong passwords.

---

## 🎯 Objectives

- Extract password hashes from password-protected PDF files.
- Use John the Ripper and Johnny for password recovery.
- Use NetworkWalks Hash Calculator and Password Cracker.
- Compare the results of different password-cracking tools and different password strengths.
- Understand the importance of strong and less predictable passwords.

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| John the Ripper | Password cracking |
| Johnny | GUI interface for John the Ripper |
| Online HashCrack PDF Hash Extractor | Extract PDF hash for JTR |
| NetworkWalks Hash Calculator | Extract PDF password hashes |
| NetworkWalks Password Cracker | Attempt password recovery |

The Week 3 JTR task specifically uses John the Ripper and Johnny to recover the password of a protected PDF. The NetworkWalks module uses the Hash Calculator followed by the Password Cracker.

---

# 🔹 Module 1 – John the Ripper / Johnny

### Methodology

1. Created/obtained a password-protected PDF.
2. Extracted the PDF password hash.
3. Saved the hash in a text file.
4. Loaded the hash into Johnny.
5. Started the password-cracking process.
6. Verified the recovered password by opening the PDF.

### Results

The three provided training PDFs were successfully recovered using Johnny.

| PDF File | Password | Result |
|---|---|---|
| My Locked PDF1 | `good-luck` | ✅ Successfully cracked |
| My Locked PDF2 | `password1` | ✅ Successfully cracked |
| My Locked PDF3 | `1qaz2wsx` | ✅ Successfully cracked |

### Observation

John the Ripper/Johnny successfully recovered the passwords from all three training PDFs.

---

# 🔹 Module 2 – NetworkWalks Tools

### Methodology

1. Uploaded the password-protected PDF to the NetworkWalks Hash Calculator.
2. Extracted the PDF hash.
3. Copied the generated `$pdf$...` hash.
4. Submitted the hash to the NetworkWalks Password Cracker.
5. Verified the recovered password by opening the PDF.

### Results

| PDF File | Password | Result |
|---|---|---|
| My Locked PDF1 | `good-luck` | ❌ Not cracked |
| My Locked PDF2 | `password1` | ✅ Successfully cracked |
| My Locked PDF3 | `1qaz2wsx` | ✅ Successfully cracked |

### Observation

The NetworkWalks Password Cracker successfully recovered the passwords for PDF2 and PDF3. PDF1 was not successfully recovered during this test.

---

# 🔹 Additional Password Strength Test

I also created two of my own password-protected PDFs to compare different password types.

### Test 1 – Stronger Custom Password

**File:** `Hack me.pdf`

**Password:** `haniahack@*3`

The password was **not successfully recovered during the test**.

### Test 2 – Simple Password

**File:** `Lets see if you can hack me.pdf`

**Password:** `password2`

The password was **successfully recovered**.

### Observation

The test demonstrated that simple and predictable passwords can be easier to recover, while a stronger and less predictable password may not be recovered during the same type of attack.

---

# 📊 Overall Results

| PDF | Password | JTR / Johnny | NetworkWalks | Flag |
|---|---|---|---|---|
| My Locked PDF1 | `good-luck` | ✅ Cracked | ❌ Not cracked | nw{cybersecurity_flag_captured_2608} |
| My Locked PDF2 | `password1` | ✅ Cracked | ✅ Cracked | nw{networkwalks_persistence_jtr_270521} |
| My Locked PDF3 | `1qaz2wsx` | ✅ Cracked | ✅ Cracked | nw{networkwalks_flag_260821_1} |
| Hack me | `haniahack@*3` | ❌ Not recovered | ❌ Not cracked | - |
| Lets see if you can hack me | `password2` | ✅ Recovered | ❌ Not cracked | - |

---

# 🔍 Key Observations

- `password1` was successfully recovered by both tools.
- The predictable password `1qaz2wsx` was also successfully recovered.
- `good-luck` was recovered using Johnny but not by the NetworkWalks Password Cracker during this test.
- The stronger custom password `haniahack@*3` was not successfully recovered during the test.
- Password complexity and predictability can affect password recovery attempts.

---

# 📚 What I Learned

Through this practical, I learned:

- How password-protected PDF hashes can be extracted.
- How to use John the Ripper and Johnny.
- How to use NetworkWalks password-cracking tools.
- How different passwords can produce different results during cracking attempts.
- Why common and predictable passwords should be avoided.
- The importance of using strong and less predictable passwords.

### Main Takeaway

> Strong and less predictable passwords provide better protection against common password-cracking attacks.

---

# 📸 Evidence

Screenshots of the practical work are included in the repository.

- PDF hash extraction
- Johnny configuration
- Password recovery results
- Successfully unlocked PDFs
- NetworkWalks Hash Calculator
- NetworkWalks Password Cracker

---

# ⚠️ Disclaimer

All password-cracking activities in this project were performed on authorized training files and PDFs created for testing purposes.

These techniques should only be used on systems and files where you have explicit permission to perform security testing.

---

# 👤 Author

**Maida Shafaq**

Cybersecurity Intern  
NetworkWalks Cybersecurity Internship

**Week 3 – Password Cracking**
