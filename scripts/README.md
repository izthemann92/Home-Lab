# 🧰 Scripts Folder
Store PowerShell, Bash, or Python scripts used in your labs.
## lab 2 install and enable ssh aon ubuntu
sudo apt update
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh

## lab 02 congifugre UFW on ubuntu
sudo apt install ufw -y
sudo ufw enable
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw status numbered

## install and enable openssh server on windows
powershell:
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automatic'
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (Port 22)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22

## connectivity Test (ubuntu -> windows)
ssh labadmin@192.168.10.11

## connectivity Test (Windows -> Ubuntu)
ssh izthemann@192.168.10.20