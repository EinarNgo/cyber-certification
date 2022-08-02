# Nessus
In this lab environment, the user is going to get access to a Kali GUI instance. An instance of the Mutillidae web application can be accessed using the tools installed on Kali at http://demo.ine.local.

Objective: Perform vulnerability scan on the target machine using Nessus.

Relevant information
- Username: admin
- Password: Adminpasswd

# 1. Browse til Nessus dashboard
Use the link: https://localhost:8834 og logging with the information from relevant information.
![nessus](nessus.png)

# 2. Scan the target machine
Enter target machine and submit
![scan](scan.png)
After submiting, follow screen should show up, then select the ip and run scan:
![host](host.png)
When the scan its finish, you will get this screen:
![finish](finish.png)
The scan discovered 2 medium severity vulnerabilities. If you want to see more information about the vulnerabilities you can click on it to see more details.

# 3. Download the report
Up in the right corner click on Report and Complete List of Vulnerabilities by Host, then generate Report.
![dwreport](dwreport.png)