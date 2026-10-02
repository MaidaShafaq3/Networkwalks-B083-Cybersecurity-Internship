# 🔐 M2 – PDF Password Recovery & Decryption

## 🎯 Objective

The objective of this task was to recover the passwords protecting three confidential patient PDF lab reports retrieved during the previous phase and successfully decrypt the files.

The three files were:

* `report_1.pdf`
* `report_2.pdf`
* `report_3.pdf`

> **Note:** The recovered passwords and confidential patient information are not included in this repository.

---

## 🔹 1. Encryption Analysis

Before attempting password recovery, the encryption settings of the PDF files were analysed using `qpdf`.

```bash
qpdf --show-encryption ~/Desktop/report_1.pdf
qpdf --show-encryption ~/Desktop/report_2.pdf
qpdf --show-encryption ~/Desktop/report_3.pdf
```

All three files were identified as encrypted PDF documents using:

* PDF Version: 1.4
* Security Handler: Standard
* Encryption Revision: R=3
* Key Length: 128-bit
* Encrypted Metadata: True

This indicated that the files were using an older standard PDF encryption scheme.

### 📸 Evidence

> ![PDF Encryption Analysis](<../Screenshots/6. PDF-Encryption-Analysis.png>)

---

## 🔹 2. Tool Selection

The following tools were used during the password-recovery process:

| Tool       | Purpose                                              |
| ---------- | ---------------------------------------------------- |
| `qpdf`     | Analyse PDF encryption and decrypt recovered files   |
| `pdfcrack` | Perform password recovery against the encrypted PDFs |
| `RockYou`  | Password wordlist used for dictionary-based recovery |
| `pdfinfo`  | Verify that the decrypted PDFs can be read           |

The RockYou wordlist was available at:

```text
/usr/share/wordlists/rockyou.txt
```

---

## 🔹 3. Report 1 Password Recovery

`pdfcrack` was used to test the RockYou wordlist against the first report:

```bash
pdfcrack -w /usr/share/wordlists/rockyou.txt ~/Desktop/report_1.pdf
```

The tool successfully recovered the user password.

### 📸 Evidence

> ![Report 1 Password Recovery](<../Screenshots/7. Report 1 Password Recovery.png>)

The recovered password is intentionally not documented in this repository.

---

## 🔹 4. Report 2 Password Recovery

The same dictionary-based approach was tested against the second report:

```bash
pdfcrack -w /usr/share/wordlists/rockyou.txt ~/Desktop/report_2.pdf
```

The password was successfully recovered.

### 📸 Evidence

> ![Report 2 Password Recovery](<../Screenshots/8. Report 2 Password Recovery.png>)

The recovered password is intentionally not documented in this repository.

---

## 🔹 5. Report 3 Password Recovery

The third report was then tested:

```bash
pdfcrack -w /usr/share/wordlists/rockyou.txt ~/Desktop/report_3.pdf
```

The password was successfully recovered.

### 📸 Evidence

> ![Report 3 Password Recovery](<../Screenshots/9. Report 3 Password Recovery.png>)

The recovered password is intentionally not documented in this repository.

---

## 🔹 6. Decryption

After recovering the passwords, `qpdf` was used to create decrypted copies of the reports.

Example:

```bash
qpdf --password='<RECOVERED_PASSWORD>' \
--decrypt ~/Desktop/report_1.pdf \
~/Desktop/report_1_decrypted.pdf
```

The same process was performed for Reports 2 and 3.

The recovered passwords were used locally and are not included in this repository.

---

## 🔹 7. Verification

The decrypted files were verified using `pdfinfo`:

```bash
pdfinfo ~/Desktop/report_1_decrypted.pdf
pdfinfo ~/Desktop/report_2_decrypted.pdf
pdfinfo ~/Desktop/report_3_decrypted.pdf
```

The PDFs were successfully opened and their contents were accessible after decryption.

### 📸 Evidence

> ![Decryption Verification](<../Screenshots/10. Decryption Verification.png>)

---

## 📊 Result

All three encrypted PDF lab reports were successfully recovered and decrypted.

| File           | Encryption Identified | Password Recovered | Decrypted |
| -------------- | --------------------- | ------------------ | --------- |
| `report_1.pdf` | ✅                     | ✅                  | ✅         |
| `report_2.pdf` | ✅                     | ✅                  | ✅         |
| `report_3.pdf` | ✅                     | ✅                  | ✅         |

### 🛠️ Tools Used

* Kali Linux
* `pdfcrack`
* `qpdf`
* `pdfinfo`
* RockYou wordlist

> **Security Note:** The original encrypted PDFs, decrypted PDFs, recovered passwords, session cookies, and any patient-identifiable information should not be committed to the public repository.


# 👤 Author

**Maida Shafaq**
