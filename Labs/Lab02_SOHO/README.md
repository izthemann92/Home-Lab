# 🧪 SOHO firewall and port fowarding 

## 🎯 Objective
simulate a small office/home office (SOHO) environement by configuring firewall rules and port fowarding between your windwows 11 and ubuntu server.

learn how network traffic moves through your router/firewall and how to control access to internal services.

Configure Ubuntu’s firewall (UFW) to restrict and allow specific network traffic

Set up port forwarding so you can reach your Ubuntu server through a designated port

🧰 Requirements

Ubuntu Server 22.04 (static IP: 192.168.10.20)

Windows 11 Pro (static IP: 192.168.10.11)

VirtualBox with NAT or Bridged networking (to simulate router or external access)

## 🧩 Steps Performed
1. Verify baseline connectivity ( Ubuntu + Windows) 
2. installed OpenSSH Server on windows 
script : Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

3. install and enable ssh on ubuntu
script: One line at a time.

sudo apt update
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh

4. lab 02 congifugre UFW on  allowing specific traffic through the firewall

sudo apt install ufw -y
sudo ufw enable
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw status numbered

5. install and enable openssh server on windows
powershell:
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automatic'
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (Port 22)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22

6. connectivity Test (ubuntu -> windows)
ssh labadmin@192.168.10.11

7. connectivity Test (Windows -> Ubuntu)
ssh izthemann@192.168.10.20

## 🧠 Troubleshooting / Notes
- Had to create seperate user known as Labadmin to properly make the connection because my microsoft orginazation was effecting the process

## 📸 Screenshots
*(Add your images in the /screenshots folder)*

## 🧾 Summary
Network was verified both directions
firwalls were configured correctly
SSH communication working between windows and ubuntu
port fowarding was succesfully simulated
