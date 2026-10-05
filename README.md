# Penetration Testing project at Mediroza Hospital
# Executive Summary

Penetration testing was carried out on Mediroza hospital to identify vulnerabilities, exploit them to demonstrate real impact, and document all findings.

This report covers my key findings, methodology, risk rating of each vulnerability, recommendations and also remediation.

• Conduct reconnaissance on the target.
• Identify exposed entry points.
• Analyse the behaviour of any authentication mechanisms you find.
• Look for weaknesses in how the application handles user input.
• Gain unauthorised access to a restricted area of the site.


# Scope and Methodology
Target - https://medirozahospital.com.

Tools used - Robots.txt, NS lookup, DNSrecon, WHOIS, Whatweb, Networkwalks Hash calculator, Networkwalks Password cracker, Command line (CMD)

I performed reconnaissance on Meridoza hospital using WHOIS, Whatweb, DNSrecon, Ns lookup. I also carried out reconnaisance on https://medirozahospital.com, using robots.txt. 
A robots.txt file tells web robots which pages or selections of a website they are allowed to visit.
Disallow entries show hidden areas of the site that the owner does not want publicly indexed.

# Username Enumeration
I opened the patient login page and typed a username and password. The response was - Username not found. I then typed username as 'admin' and entered a password. The response was -incorrect password.
The site gave two different messages. The second confirmed admin as a real account. This shows a vulnerability, a secure login should always show the same message, regardless of which field is wrong.

# Test for SQL injection
I typed a single quote in the username field - admin' 
Username: admin'
Password: 123456
The error message displayed comfiems that the login is vulnerable to SQL injection (Warning: )


<img width="911" height="821" alt="Screenshot 2026-10-01 181557" src="https://github.com/user-attachments/assets/b7dfd414-bf6a-4c3d-9ba4-1c459e819597" />





# Findings and Proof of Exploitation
Each vulnerability with screenshots and evidence for every milestone.


# Risk Rating
Rate each vulnerability: Critical, High, Medium or Low with justification.


# Recommendations and Remediation
Actionable steps the client should take to fix each identified
