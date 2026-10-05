<img width="983" height="858" alt="Patient Laboratory report 1" src="https://github.com/user-attachments/assets/3579787e-1b35-4265-97cd-eac2fcf00ee3" /># Penetration Testing project at Mediroza Hospital
# Executive Summary

Penetration testing was carried out on Mediroza hospital to identify vulnerabilities, exploit them to demonstrate real impact, and document all findings.

This report covers my key findings, methodology, risk rating of each vulnerability, recommendations and also remediation.

# Scope and Methodology
Target - https://medirozahospital.com.

Tools used - Robots.txt, NS lookup, DNSrecon, WHOIS, Whatweb, Networkwalks Hash calculator, Networkwalks Password cracker, Command line (CMD), Exiftool.exe.

I performed reconnaissance on Meridoza hospital using WHOIS, Whatweb, DNSrecon, Ns lookup. I also carried out reconnaisance on https://medirozahospital.com, using robots.txt. 

A robots.txt file tells web robots which pages or selections of a website they are allowed to visit.
Disallow entries show hidden areas of the site that the owner does not want publicly indexed.


<img width="525" height="267" alt="Robots txt" src="https://github.com/user-attachments/assets/b9c9f08c-e02b-4796-a545-adba7df905b6" />


# Findings and Proof of Exploitation

Username Enumeration

I opened the patient login page and typed a username and password. The response was - Username not found. I then typed username as 'admin' and entered a password. The response was -incorrect password.
The site gave two different messages. The second confirmed admin as a real account. This shows a vulnerability, a secure login should always show the same message, regardless of which field is wrong.

Test for SQL injection

I typed a single quote in the username field - admin' 
Username: admin'
Password: 123456
The error message displayed comfiems that the login is vulnerable to SQL injection

<img width="911" height="821" alt="Screenshot 2026-10-01 181557" src="https://github.com/user-attachments/assets/b7dfd414-bf6a-4c3d-9ba4-1c459e819597" />

The payload (admin' -- ) works by breaking out of the query string with a quote, then using '--' to comment out everything after it, which also includes the password check. the database matches admin with no password condition.

After inputing the payload, I gained access into the web application. Then proceeded to download three patient encrypted laboratory results.

<img width="1724" height="720" alt="Screenshot 2026-10-03 120640" src="https://github.com/user-attachments/assets/f753a028-804a-41fb-9017-b6178c6b6eae" />

I downloaded the Encrypted PDF files to be able to decrypt them. To crack the password, Networkwalks hash calculator was used to extract the hash and then the cracking tool then tried passwords from a wordlist and checks each one against the hash.

If the wordlist is exhausted and password is still not found, try a larger wordlist, whick is what I did.

I was able to crack all three locked PDFs, and their passwords extracted to gain access to the patients laboratory results. 

<img width="1028" height="907" alt="Screenshot 2026-10-03 123355" src="https://github.com/user-attachments/assets/5a57de85-8b8c-43ca-a5b6-844fda7bfbd2" />

<img width="1112" height="925" alt="Screenshot 2026-10-03 132905" src="https://github.com/user-attachments/assets/d4cb234b-a0fa-43f1-b1fc-9e4afcef1eef" />

<img width="983" height="858" alt="Patient Laboratory report 1" src="https://github.com/user-attachments/assets/be9ffd5f-35c4-4979-abc8-406c90e2139e" />

<img width="1000" height="856" alt="Patient Laboratory report 2" src="https://github.com/user-attachments/assets/590a3c42-26e4-4d66-acff-e0a2027643d5" />

<img width="1032" height="856" alt="Patient Laboratory report 3" src="https://github.com/user-attachments/assets/78373915-d439-4e18-a648-5e42fd9cff37" />

Deep Reconnaissance

I read the metadata using exiftool - a command line tool that reads and displays all metadata fields from any file type including PDFs (Metadata is hidden information stored inside a file, such as who created it, when, and with what software)

I ran the exiftool command (exiftool patient_laboratory_report_1.pdf) to get metadata about the patients report. 

<img width="939" height="1018" alt="Exiftool" src="https://github.com/user-attachments/assets/cb15430b-41c1-4a30-a340-612d8f9bb851" />

To get more information, I had to use the password option (exiftool -password your_password) to unlock other parts of the data.  I was able to uncover the name of the Author - J. Malik and other details and backup data that has been moved to an old site.

Further reconnaissance exposed a directory listing which exposed Staff name, salaries and shareholders information. 
I copied this information to chatGPT to generate a readable table and also generate PDF copies of these tables.
The name Jameel Malik is also in the staff table. Recall that the same name (J. Malik) moved the backup and left the note inside the file.

# Risk Rating
| Vulnerability | Location | Risk
| :--- | :--- | :---
| Weak PDF passwords crackable with a wordlist | 'patient_laboratory_report_1.pdf' | High |
| Confidential Staff salaries and shareholders data exposed | 'old/mediroza_db_backup_2019.sql' | Critical
 




# Recommendations and Remediation
Actionable steps the client should take to fix each identified
