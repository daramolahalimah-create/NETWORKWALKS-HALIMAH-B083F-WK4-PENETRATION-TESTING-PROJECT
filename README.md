# PENETRATION TESTING PROJECT.
## PENETRATION TESTING, MEDIROZA HOSPITAL.
 ### W3-PM-FINAL | CYBERSECURITY | NETWORKWALKS

 | FIELD | DETAILS |
 |---|---|
 | Pentester name | Halimah Daramola|
 | Program/Batch | B083F-Networkwalks |
 | Date | 08 October 2026 |
 | Modules Completed | W4 (Penetration Testing project) |
 | Client/Target | Mediroza Hospital | 
 | Permission secured from client | Yes |
 | Phases covered | Phase 1; Initial Access   Phase 2; Data Extraction  Phase 3; Attack ( Cracking) |


 ---

### 1. Liability Disclaimer

I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged

---

### 2. Introduction 
This report covers full-black box penetration testing & vulnerability assessment on Mediroza Hospital. This report shows the attack on the mediroza hospital website which includes; gaining access and retrieving 3 confidential patient PDF lab reports, cracking of all 3 encrypted files and finding the details of staff salaries and shareholders.

---
### 3. Tools Used
|Tools | Purpose|
|---|---|
| Windows & Kali | Operating systems used for penetration testing|
| Networkwalks Hash Calculator | hash out all encrypted files |
| Networkwalks Password Cracker | crack all hashed files to reveal the passwords|
| Github | SQL Injection source |

---
### 4. Activities Conducted 
**4.1 Milestone 1**
- I used **Zenmap** to performed reconnaissance on the target. The results showed two openned ports ( 80 & 443 tcp ports) which can allow SQL injections.
- I then openned the payload all things Github page. The results showed all possible SQL injections. 
- I inputed **'or 1=1 limit 1--** into the username and password column to login into the patient portal. The result gave a warning **mysqli_query(): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near "or 1=1 limit 1--' at line 1**.
- I used **admin'--** as both username and password to login the patient portal. The result revealed 3 patient lab reports which i downloaded


**4.2 Milestone 2**
- I used **Networkwalks hash calculator** to extract the hash value of each file. The result shows the hahe result showed the hashed values of the files
- I then copied the full hash value and and ran it in **networkwalk password cracker**. The result revealed the password of the encrypted files.
- I then used the password to open the files. The result revealed the test results.

**4.3 Milestone 3**
- I used **exiftool unlocked_patient_report_3.pdf** to read the metadata of the patient report 3. The result showed hidden informations of the pdf file, including a robot file that point to /old.
- I then downloaded the file by going to **https://medirozahospital.com/old/** which revealed the backup file **mediroza_db_backup_2019.sql**
- I used chatGPT to open the file . The result showed list of shareholders.

### 5. Risk Analysis/Impact
| # | Risk | Evidence | Potential Impact | Risk Level |
|---|---|---|---|---|
|1.| Web application vulnerabilities | Open HTTP/HTTPS ports (80 & 443) | Allows unauthenticated users to interact directly with backend database, bypass security controls, and extract sensitive information | High |
|2.| Authentication bypass & weak access control | Successful login to the patient portal using SQL injection payloads without valid user credentials | Unauthorized access to protected system areas, administrative features and confidential patient records | Critical |
|3.| Confidential patient data exposure | Downloading 3 confidential patient lab reports from the patient portal following authentication bypass | Severe breach of patient privacy, potential regulatory non-compliance and  reputational damage | Critical |
|4.| Weak password hashing and cracking | Successfully extracted file hashes using Networkwalks Hash Calculator and cracked them via Networkwalks Password Cracker to reveal plain-text passwords | Encrypted medical test results and sensitive files can be easily decrypted and viewed by unauthorized parties once accessed | Medium |
|5.| Insecure storage and lack of post-exfiltration security controls | Downloaded patient records stored without supplementary encryption layers or access restriction controls post-download | Persistence of exposure; if a workstation or server directory is compromised, sensitive medical documents remain instantly readable to attackers without secondary decryption hurdles | High|

---

### 6. Recommendations 
- Implement Parameterized Queries / Prepared Statements: Update the backend database queries to use prepared statements (PDO or parameterized MySQLi) to prevent user input from being interpreted as executable SQL code.

- Input Validation & Sanitization: Enforce strict input validation on all web forms and entry fields to sanitize special characters before processing requests.

- Disable Verbose Error Messages: Configure the web server and database to hide detailed error messages (mysqli_query() errors) from end users to prevent information disclosure.

- Upgrade Encryption Standards: Replace weak password hashing algorithms with strong, modern key-derivation functions such as bcrypt or Argon2 to protect stored files against offline cracking.

- Access Control & Rate Limiting: Implement strict session management, role-based access controls, and rate limiting/account lockout policies to defend against automated payload attempts.
  
- Secure Post-Download Storage & Data-at-Rest Protection : Ensure that exported or downloaded sensitive reports utilize robust file-level encryption (such as AES-256) and strict access permission configurations to secure data even outside the active web boundary.

---

### 7. Conclusion
During week 4 of my Cybersecurity & Ethical Hacking Internship, i successfully completed penetration testing assessment on the target patient portal application across two major project milestones. In Milestone 1, network reconnaissance revealed open HTTP/HTTPS ports (80 & 443), and using SQL injection payloads ('or 1=1 limit 1-- and admin'--), I bypassed authentication controls and exfiltrated three confidential patient lab reports. In Milestone 2, I extracted the file hashes using the Networkwalks Hash Calculator and cracked them with the Networkwalks Password Cracker to reveal the plain-text passwords and open the test results. In Milestone 3, I analyzed post-exfiltration data handling, exposing risks associated with unencrypted local storage of downloaded files.Addressing these findings by enforcing input sanitization, adopting parameterized queries, suppressing database error messages, and upgrading file encryption—will eliminate the identified attack vectors, strengthen the system’s security posture, and ensure regulatory compliance such as HIPAA.

---

### 8. Evidence Collected

<img width="952" height="497" alt="Screenshot 2026-10-10 223842" src="https://github.com/user-attachments/assets/0a6c56cb-a3a7-4d08-ba13-40aae421d47b" />

<img width="1255" height="783" alt="Screenshot_2026-10-06_10-06-34" src="https://github.com/user-attachments/assets/38709ca7-16a3-45ec-aca3-702353ed1e8f" />

<img width="1271" height="797" alt="Screenshot_2026-10-06_10-08-20" src="https://github.com/user-attachments/assets/3ead3b95-08d0-45de-8840-0ef733d79503" />

<img width="1266" height="785" alt="Screenshot_2026-10-06_10-08-55" src="https://github.com/user-attachments/assets/b89a9b73-ab65-4415-a2a7-54680d02b698" />

<img width="1272" height="795" alt="Screenshot_2026-10-06_10-07-31" src="https://github.com/user-attachments/assets/a497ef5d-ad76-4119-b1bb-5aea61131ce8" />

<img width="1268" height="797" alt="Screenshot_2026-10-06_10-11-33" src="https://github.com/user-attachments/assets/562aefe7-2c88-4f7b-a414-d44f86c4e5b4" />

<img width="1274" height="797" alt="Screenshot_2026-10-06_10-16-16" src="https://github.com/user-attachments/assets/f852a085-2f7d-4ec8-8863-2258fc6ef651" />

<img width="1703" height="960" alt="Screenshot 2026-10-06 155144" src="https://github.com/user-attachments/assets/7de275b9-827b-4a93-bd67-4100b47d1fd9" />

<img width="1841" height="945" alt="Screenshot 2026-10-06 155314" src="https://github.com/user-attachments/assets/cb5832f8-edb3-43f3-b5a0-c4a709554820" />

<img width="1427" height="826" alt="Screenshot 2026-10-07 154908" src="https://github.com/user-attachments/assets/4a5ae617-5c40-46fa-ba69-26799b89dbb3" />

<img width="1497" height="876" alt="Screenshot 2026-10-07 155120" src="https://github.com/user-attachments/assets/acfb5f79-9598-4a5c-b9a8-f78235c069da" />

<img width="1437" height="823" alt="Screenshot 2026-10-07 155744" src="https://github.com/user-attachments/assets/061fcf2f-53f8-439b-81e6-f15e1c2bf3ee" />

<img width="941" height="888" alt="Screenshot 2026-10-07 160246" src="https://github.com/user-attachments/assets/929be1a3-7071-4e5b-8036-d332a59db62d" />

<img width="958" height="1002" alt="Screenshot 2026-10-07 160313" src="https://github.com/user-attachments/assets/7ba55f63-1840-410a-ad2e-7752fd3397bf" />

<img width="939" height="884" alt="Screenshot 2026-10-07 160656" src="https://github.com/user-attachments/assets/3103a79f-6c8b-410f-af20-d8c43eaa1855" />

<img width="927" height="825" alt="Screenshot 2026-10-07 160719" src="https://github.com/user-attachments/assets/e98c4b31-57ff-47af-ae42-b097d9a9abe1" />

<img width="918" height="892" alt="Screenshot 2026-10-07 160855" src="https://github.com/user-attachments/assets/9d1cc06c-ee69-4cca-83cd-22d2fd3afebb" />

<img width="895" height="824" alt="Screenshot 2026-10-07 160919" src="https://github.com/user-attachments/assets/be69a258-ec7e-4266-816a-1ee3c07f48e7" />



