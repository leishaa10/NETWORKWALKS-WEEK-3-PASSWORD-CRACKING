# PDF Password Security: Hash Extraction, Analysis & Dictionary Attacks

**Cybersecurity Internship | Networkwalks | Week 03**

## 1. Project Overview

This repository documents my Week 03 practical exercises on PDF password security, hash extraction, and dictionary-based password auditing as part of the Networkwalks Cybersecurity Internship.

The objective of this exercise was to understand how password-protected PDF documents store their encryption-related information, how password hashes can be extracted, and how password auditing tools can test candidate passwords against those hashes.

Rather than attempting to directly bypass PDF encryption, the exercises focused on understanding the password verification process through extracted hashes and controlled dictionary-based testing.

I explored two aspects of the workflow:

**Module 1: John the Ripper and Johnny GUI**

Understanding the installation, configuration, and use of John the Ripper through its graphical interface, Johnny. This included configuring the executable, loading an extracted PDF hash, running a dictionary-based attack, and recovering the password.

**Module 2: Networkwalks Hash Analysis Tools**

Using the Networkwalks Hash Calculator to extract an encrypted PDF's hash and the Networkwalks Comparison Tool to perform dictionary-based password comparison. I also explored Online Hash Crack as an additional PDF hash extraction utility.

### Objectives

- Understand the fundamentals of password-protected PDF documents.
- Learn the difference between a plaintext password and its extracted hash representation.
- Explore PDF hash extraction techniques.
- Configure John the Ripper and connect it with Johnny GUI.
- Understand how dictionary-based password attacks work.
- Compare password candidates against extracted PDF hashes.
- Observe how weak and predictable passwords affect document security.
- Verify the outcome of the practical exercise through successful document access and flag capture.

---

## 2. Lab Environment

| Parameter | Details |
|---|---|
| Trainee | Leisha Santoshkumar |
| Internship Organization | Networkwalks |
| Program/Batch | 084C |
| Internship Week | Week 03 |
| Operating System | Windows |
| Domain | Cybersecurity & Ethical Hacking |
| Primary Tool | John the Ripper (Jumbo) |
| Graphical Interface | Johnny |
| Hash Extraction | Networkwalks Hash Calculator |
| Additional Extraction Utility | Online Hash Crack |
| Comparison Tool | Networkwalks Comparison Tool |
| Verification Tool | Adobe Acrobat / Edge PDF Viewer |
| Target File Type | Password-protected PDF |
| Date | 17 November 2026 |

### Test Documents Used

Two separate password-protected PDF documents were used for the practical exercises:

- **Module 1:** `My Locked PDF1.pdf` – Used for PDF hash extraction and password auditing through John the Ripper with Johnny GUI.
- **Module 2:** `My Locked PDF2.pdf` – Used for PDF hash extraction through the Networkwalks Hash Calculator and subsequent dictionary-based comparison using the Networkwalks Comparison Tool.
  
---

## 3. Module 1: John the Ripper with Johnny GUI

### 3.1 Tools and Technologies

**John the Ripper (Jumbo Edition)**

John the Ripper is an open-source password security auditing tool. It supports multiple password hash formats and different testing techniques, including dictionary-based password testing.

The Jumbo edition provides additional format and feature support compared with the core version.

**Johnny GUI**

Johnny is a graphical front-end for John the Ripper. It allows users to configure and operate the underlying auditing engine through a visual interface rather than relying entirely on command-line instructions.

**PDF Hash Extraction Utility**

A compatible extraction utility is required to convert the protected PDF's password-verification information into a format that John the Ripper can process.

### 3.2 Practical Implementation

**Step 1: Downloading and configuring John the Ripper**

Downloaded the Windows 64-bit Jumbo build of John the Ripper and extracted its contents.

The main executable required for Johnny integration is:

`john.exe`

It is located inside the extracted `run` directory, at the path:

`C:\Users\DELL\Downloads\john-1.9.0-jumbo-1-win64\john-1.9.0-jumbo-1-win64\run\john.exe`

**Step 2: Linking Johnny with John the Ripper**

Navigated to the Settings section in Johnny.

Used the Browse option to locate the `john.exe` executable and selected it.

Johnny successfully detected the installed version:

`John the Ripper 1.9.0-jumbo-1 OMP [cygwin 64-bit x86_64 AVX2 AC]`

This confirmed that the graphical interface could communicate with the underlying password auditing engine.

**Screenshot: `01-johnny-settings-configured.png`**

<img width="867" height="685" alt="nw week3 ss1" src="https://github.com/user-attachments/assets/25676465-e18d-48a6-aa21-600adc93c571" />

**Observation:** Correct executable configuration is essential because Johnny acts as an interface, while John the Ripper performs the actual password auditing operations.

**Step 3: Extracting the PDF hash**

Selected the authorized encrypted PDF training document and used a PDF hash extraction utility to obtain its hash representation.

The resulting hash followed the specialized PDF format:

`$pdf$4*4*128*-102...`

This representation contains the information needed by compatible password auditing tools to test password candidates.

**Step 4: Loading the extracted hash into Johnny**

Opened the password file containing the extracted hash using the **Open password file** option.

Selected the appropriate input format and loaded the file into Johnny.

The application displayed the loaded entry in the Passwords section with the hash populated and the format correctly identified as **PDF**. At this stage the Password column was still empty, and the status bar showed `0% (0/1: 0 cracked, 1 left) [format=PDF]`.

**Screenshot: `02-johnny-pdf-hash-loaded.png`**

<img width="947" height="681" alt="Screenshot 2026-11-17 133625" src="https://github.com/user-attachments/assets/4a7190d2-7770-4db1-815e-257d800dfc3e" />

**Step 5: Running the dictionary attack**

With the hash loaded, used the **Start new attack** option in Johnny to begin a dictionary-based attack against the loaded `$pdf$` hash, relying on John the Ripper's underlying engine to perform the comparison.

**Step 6: Successful password recovery**

The attack completed with the hash successfully cracked. Johnny displayed the recovered password directly in the Password column:

`good-luck`

The status bar updated to `100% (1/1: 1 cracked, 0 left) [format=PDF]`, confirming that the single loaded hash had been fully cracked.

**Screenshot: `03-johnny-attack-cracked.png`**

<img width="800" height="768" alt="Screenshot 2026-11-16 221711" src="https://github.com/user-attachments/assets/51717afb-0d96-4759-8e38-e083d956a891" />

**Step 7: Flag capture for Module 1**

Upon confirming the recovered password, the Networkwalks training platform displayed a completion confirmation for this practical:

`nw{cybersecurity_flag_captured_2608}`

**Screenshot: `04-jtr-flag-captured.png`**

<img width="1857" height="907" alt="Screenshot 2026-11-16 221443" src="https://github.com/user-attachments/assets/610d35b7-bb88-4703-a605-8683707a0bfe" />

<img width="617" height="857" alt="nw week 3 ss4" src="https://github.com/user-attachments/assets/87042d91-4f9e-4573-960a-1e5bc522b24f" />


**Module 1 Observation**

This module helped me understand the complete relationship between a graphical password auditing interface and its underlying engine — not only configuring and loading a hash, but actually executing the attack end to end and observing a successful crack. It also demonstrated why identifying the correct hash format and configuring the executable are important before beginning a password security assessment.

---

## 4. Module 2: PDF Hash Extraction Using Networkwalks Tools

### 4.1 Tools Used

**Networkwalks Hash Calculator**

A browser-based utility that supports generating hashes from text and files, as well as extracting password hashes from encrypted PDF documents.

The interface indicates that PDF parsing is performed locally in the browser.

**Networkwalks Comparison Tool**

A password comparison utility that accepts an extracted PDF hash and tests candidate values against a built-in dictionary.

**Online Hash Crack**

An additional online PDF hash extraction utility that generates password hash representations compatible with tools such as `pdf2john` and Hashcat.

### 4.2 Practical Implementation

**Step 1: Accessing the Networkwalks Hash Calculator**

Opened the Networkwalks Hash Calculator.

The tool provides three different input modes:

- Text: Generates supported cryptographic hashes from text input.
- File: Processes file input for supported hash operations.
- PDF: Extracts password-related hash information from encrypted PDF documents.

Selected the **PDF** tab to begin the document security exercise.

**Step 2: Selecting the encrypted PDF**

Selected the password-protected training document (`My Locked PDF2.pdf`, 204.7 KB) from the local system.

The calculator processed the document and detected that it was encrypted, displaying:

> "This PDF is encrypted. A crackable hash has been extracted below (pdf2john / hashcat compatible format)."

It then generated a PDF hash representation in a format compatible with PDF password auditing utilities.

The tool displayed the following technical parameters:

| Parameter | Observed Value |
|---|---|
| Document Type | Encrypted PDF |
| Hash Format | PDF / pdf2john-compatible |
| Revision | R4 |
| PDF Version | V4 |
| Encryption Key Length | 128 bit |

These parameters help identify the encryption configuration associated with the document.

**Screenshot: `05-hash-calculator-pdf-tab.png`**

<img width="902" height="500" alt="image" src="https://github.com/user-attachments/assets/3a53c4e0-ecfd-4bf5-b9dd-36607403f902" />

**Step 3: Understanding the extracted PDF hash**

The extracted `$pdf$...` string represents the information required for password verification by compatible auditing tools.

The extracted value is not the original password. It acts as the input for subsequent password candidate testing.

The extraction stage is therefore separate from the password comparison stage.

**Step 4: Exploring Online Hash Crack**

To understand another approach to PDF hash extraction, I also used Online Hash Crack's **PDF Hash Extractor** tool ("Extract a PDF hash for a controlled test").

Selected an encrypted PDF (`My Locked PDF2.pdf`) through its interface and clicked **Choose file**.

The utility processed the selected document and displayed an extraction-completed message:

> "Extraction complete. Review the output before using it in an authorized test."

Its output was intended for use with compatible PDF password auditing tools, including `pdf2john` and Hashcat. The site also noted that uploaded files are processed for extraction and then deleted, with a 100 MB maximum upload size.

**Screenshot: `06-online-hashcrack-extraction.png`**

<img width="1142" height="911" alt="nw week 3 ss5" src="https://github.com/user-attachments/assets/8cc57de2-9e6e-4276-97a4-ff571e018c5e" />

**Step 5: Opening the Networkwalks Comparison Tool**

After extracting the hash using the Networkwalks Hash Calculator, accessed the Comparison Tool (the "Password Cracker through Dictionary Attacks" lab).

The tool accepts the extracted PDF hash as input and uses a predefined dictionary of candidate passwords for comparison, following the same conceptual approach as John the Ripper.

**Step 6: Submitting the hash for comparison**

Pasted the extracted PDF hash into the appropriate input field.

Initiated the comparison process using the tool's built-in candidate password list (100 candidates total).

The interface displayed, in real time:

- Number of candidate values attempted (progress bar).
- Total dictionary size.
- Processing speed (password attempts per second).
- Overall progress percentage.
- Individual password candidates being tested, such as `secret`, `pepper`, `ginger`, `maggie`, `access`, `flower`, `cookie`, `banana`, `orange`, `purple`.

During the observed run, the interface displayed 91 out of 100 candidates attempted, corresponding to 91% progress, at a rate of roughly 9 passwords/second.

**Step 7: Observing the successful match**

The comparison tool went on to display a **"Password Cracked Successfully"** notification, with instructions to open the PDF and enter the recovered value to unlock the file. The matched password itself has been redacted in the repository screenshot.

**Screenshot: `07-comparison-tool-dictionary-attack.png`**

<img width="1012" height="781" alt="nw week3 ss6" src="https://github.com/user-attachments/assets/35ddbf46-c92e-4949-9c2e-90415974ce55" />

**Step 8: Flag capture for Module 2**

After successfully completing the assigned password security exercise, the Networkwalks training platform displayed a completion confirmation:

`nw{networkwalks_persistence_jtr_270521}`

**Step 9: Verifying the recovered password**

Used the recovered password to open the corresponding password-protected training document in a PDF viewer. The viewer's **"Enter a password"** prompt accepted the recovered value and unlocked the document.

**Screenshot: `08-nw-flag-captured.png`**

<img width="1857" height="907" alt="Screenshot 2026-11-16 221443" src="https://github.com/user-attachments/assets/2c733fcb-ed40-42a2-b3fd-c9f191b3715f" />

**Screenshot: `09-pdf-password-verification.png`**

<img width="492" height="707" alt="nw week3 ss7" src="https://github.com/user-attachments/assets/812aa2f4-3251-4789-a588-aa9cd44b60a2" />

Successful access confirmed that the password identified by the comparison process was valid for the test document. This verification step is important because it confirms the practical result rather than relying only on the tool's success notification.

**Module 2 Observation**

The exercise demonstrated the complete workflow of extracting a PDF hash, supplying it to a comparison utility, testing dictionary candidates, observing a successful match, and verifying access against the real document.

It also highlighted the importance of choosing compatible hash formats when moving between extraction and password auditing tools.

---

## 5. Flag Capture and Completion

This practical produced **two separate flags**, one per module:

| Module | Tool Chain | Flag |
|---|---|---|
| Module 1 | John the Ripper + Johnny |  `nw{cybersecurity_flag_captured_2608}`  |
| Module 2 | Networkwalks Hash Calculator + Comparison Tool | `nw{networkwalks_persistence_jtr_270521}` |

Both completion screens confirmed that their respective flags had been successfully captured, marking the completion of both practical exercises.

---

## 6. Comparative Analysis of the Tools

The practical involved multiple utilities, each serving a different purpose in the password auditing workflow.

| Tool | Primary Function | Practical Application |
|---|---|---|
| John the Ripper | Password auditing engine | Processes hashes and tests password candidates |
| Johnny | Graphical interface | Configures, manages, and runs John the Ripper; displayed the recovered password (`good-luck`) directly |
| Networkwalks Hash Calculator | Hash extraction and generation | Extracts password-related information from encrypted PDFs (`My Locked PDF2.pdf`) |
| Networkwalks Comparison Tool | Dictionary comparison | Tests candidate passwords against extracted hashes, with live progress and speed metrics |
| Online Hash Crack | PDF hash extraction | Generates compatible PDF hash representations (`My Locked PDF1.pdf`) |
| Adobe Acrobat / Edge PDF Viewer | Verification | Confirms the recovered password actually unlocks the original document |

### Understanding the Difference Between Extraction, Cracking, and Verification

One of the most important concepts learned during this exercise is that hash extraction, password recovery, and verification are three separate operations.

**Hash Extraction**

The extraction utility reads the encrypted PDF and produces a representation of its password-verification information.

**Password Auditing**

The auditing tool takes the extracted representation and checks possible password candidates against it.

**Password Verification**

The recovered candidate is tested against the original document to confirm whether it successfully unlocks the PDF.

Understanding these separate stages makes the overall password auditing workflow easier to follow.

---

## 7. Key Observations and Results

The following observations were made during the practical exercises:

1. Johnny requires a correctly configured John the Ripper executable before it can use the underlying auditing engine.
2. The extracted PDF hash must be loaded in a compatible format for password auditing.
3. PDF hashes use a specialized representation (`$pdf$4*4*128*-102...`) and should not be confused with ordinary MD5 or SHA hash outputs.
4. Dictionary attacks work by testing predefined candidate values rather than generating every possible password combination.
5. Johnny successfully cracked the loaded PDF hash using a dictionary attack, recovering the password `good-luck` and updating its status bar to `100% (1/1: 1 cracked, 0 left)`.
6. The Networkwalks Comparison Tool displayed its progress (91/100 candidates, 91%) and processing speed (9 pw/s) during testing.
7. A successful match indicates that a candidate from the tested dictionary corresponds to the protected document's password.
8. Verifying the recovered value against the original PDF (via the PDF viewer's password prompt) provides confirmation of the result.
9. Password predictability can significantly reduce the practical security of an encrypted document.

---

## 8. Key Learnings

This practical exercise helped strengthen my understanding of several cybersecurity concepts.

**1. Password Security and Encryption**

Understood how document encryption and password verification work together to protect sensitive information.

**2. Hash Extraction Techniques**

Learned how password-related information can be extracted from encrypted PDF files and converted into a format supported by auditing tools.

**3. Working with John the Ripper**

Gained practical exposure to configuring John the Ripper Jumbo, integrating it with the Johnny graphical interface, and running a complete dictionary attack to successful completion.

**4. Dictionary-Based Password Auditing**

Understood how password candidates are systematically compared against extracted hash information, both via a GUI tool (Johnny) and a browser-based comparison tool.

**5. Understanding Hash Formats**

Learned that different applications require compatible hash representations, making correct format identification an important part of the auditing process.

**6. Practical Tool Integration**

Explored how different tools can be used together to perform different stages of a password security assessment — extraction, cracking, and verification.

**7. Importance of Strong Passwords**

Observed why passwords based on common words, predictable patterns, or frequently used combinations (e.g., `good-luck`) are more susceptible to dictionary-based attacks.

**8. Responsible Security Testing**

Understood the importance of performing password audits only on personal documents, authorized training files, or systems for which explicit permission has been granted.

---

## 9. Security Recommendations

Based on the observations from this exercise, the following practices can help improve PDF password security:

- Use long, unique, and unpredictable passwords.
- Avoid dictionary words, commonly used passwords, and personal information.
- Do not reuse passwords across multiple documents or accounts.
- Use appropriate PDF encryption settings and modern security-supported software.
- Store document passwords securely rather than sharing them through unprotected channels.
- Periodically review the protection applied to sensitive documents.
- Perform password security assessments only with appropriate authorization.

A strong encryption mechanism is important, but password selection also plays a significant role in the overall security of a protected document.

---

## 10. Conclusion

The Week 03 practical provided hands-on exposure to PDF password security and the process of extracting, analyzing, and cracking password hashes.

Through John the Ripper and Johnny, I explored the configuration of a password auditing environment, loaded an extracted PDF hash, ran a complete dictionary attack, and recovered the password (`good-luck`) directly within the GUI.

Through the Networkwalks Hash Calculator and Comparison Tool, I followed the workflow of extracting a PDF hash, testing dictionary-based password candidates, observing a successful match, capturing a flag, and verifying access to the protected document using a PDF viewer.

I also explored Online Hash Crack to understand an alternative PDF hash extraction workflow.

Overall, this exercise helped me connect theoretical concepts such as encryption, hashing, password verification, and dictionary attacks with practical cybersecurity tools, and to carry the workflow through to a verified, end-to-end result.

It reinforced an important security lesson: protecting a document requires not only appropriate encryption but also a strong and unpredictable password.

---

## 11. Disclaimer

This repository is maintained for educational and documentation purposes as part of the Networkwalks Cybersecurity Internship.

All practical activities were conducted within an authorized learning environment using designated training documents.

The techniques demonstrated here are intended for legitimate password security auditing and awareness. They must not be used to access, analyze, or recover passwords from documents without the owner's permission or appropriate authorization.

---

## 12. Author Information

**Leisha Santoshkumar**

Cybersecurity Intern | Networkwalks

| Detail | Information |
|---|---|
| Program | Networkwalks Cybersecurity Internship |
| Batch | 084C |
| Week | 03 |
| Domain | Cybersecurity & Ethical Hacking |
| Practical Topic | PDF Hash Extraction and Dictionary-Based Password Auditing |

**Repository Purpose:** Documentation of Week 03 practical implementation, technical observations, and cybersecurity learnings.
