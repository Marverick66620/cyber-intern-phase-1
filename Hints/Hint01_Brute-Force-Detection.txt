1. Brute Force Detection
Hint:
Look into authentication logs like /var/log/auth.log or Windows Event ID 4625. Focus on patterns where
multiple failed attempts are made from the same IP in a short time.
Tip: Think of Hydra or Burp Suite brute force modules.
What to do:
• Create a fake RDP login attempt using the following:
for ($i=1; $i -le 10; $i++) {
 net use \\127.0.0.1\IPC$ /user:FakeUser WrongPassword
}
What gets logged:
• Windows Event ID 4625 (Failed Logon)
• Sysmon may capture process and network-related activity
