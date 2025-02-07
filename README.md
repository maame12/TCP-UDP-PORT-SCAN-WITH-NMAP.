# TCP AND UDP-PORT-SCAN-WITH-NMAP.

## 1. What is NMAP?
NMAP is a security tool used to discover open ports and services and discover vulnerabilities in a network.

## 2. Objective
This project is to scan a remote machine, to discover open ports and running services.

## 3. Prerequisites
- **VMWare** or **Virtual Box** installed on your device.
- Two **Kali Linux** machines installed on your system (NB: One will be the target machine and the other the attacker machine).
- Use a "NAT Network" adapter for the two machines. Link to setup: [NAT NETWORK](https://youtu.be/X-uBoEW9H2Q?si=6NuuvMVh9xctIHyJ)

## 4. Installing and Configuring the VMs
### <ins>Configuring the target VM.</ins>
#### Step1: Update your Kali Linux
This ensures that your machine has the latest updates and security patches.
``` bash
sudo apt update && sudo apt upgrade -y
```
#### Step2: Install a service Eg. SSH which uses TCP as its transport protocol, and SNMP which uses UDP as its transport protocol
(NB.You can skip this if you have any service already running on your machine)
``` bash
sudo apt install openssh-server
```
#### Step3: Start the SSH service.
``` bash
sudo systemctl start ssh
```
#### Step4: Check the status of the service. If the service is working, you should see ***active(running)***
``` bash
sudo systemctl status ssh
```
#### Step5: Install SNMP
``` bash
sudo apt-get install snmpd snmp snmp-mibs-downloader 
```
#### Step6: Using a text editor configure SNMP, 
``` bash
sudo nano /etc/snmp/snmpd.conf
```
Add the following instructions:
- rocommunity public
- agentAddress udp:161

#### Step7: Restart the service
``` bash
sudo systemctl restart snmpd
sudo systemctl enable snmpd
```
### Step8: Check the status of the service. If the service is working, you should see ***active(running)***
``` bash
sudo systemctl status snmpd
```
  
#### Step8: Check the IP address of the machine.
``` bash
ifconfig
```
## Performing TCP scan using attacker VM.
#### Step1: You can ping the target machine to check is it's UP.
``` bash
ping <target_ip_address>
```
#### Step2: If the machine is UP you can go ahead and scan using NMAP.
``` bash
nmap <target_ip_adress>
```
You can also scan for all TCP ports available on the machine.
``` bash
nmap <target_ip_address> -p-
```

## Performing UDP scan using attacker VM.
#### Step1: You can ping the target machine to check is it's UP.
``` bash
ping <target_ip_address>
```
#### Step2: If the machine is UP you can go ahead and scan using NMAP.
``` bash
nmap -sU <target_ip_adress>
```
You can also scan for all TCP ports available on the machine.
``` bash
nmap -sU <target_ip_address> -p-
```
For more information on commands, check out [NMAP COMMANDS](https://www.stationx.net/nmap-cheat-sheet/)








