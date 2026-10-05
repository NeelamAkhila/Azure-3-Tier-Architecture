# Azure-3-Tier-Architecture
This project demonstrates the implementation of a 3-Tier Architecture on Microsoft Azure using separate Virtual Machines for the Web, Application, and Database layers.  The architecture is designed to provide secure communication between the tiers while restricting direct access between the Web and Database layers.

🏗️ Architecture

The project consists of three tiers:

Web Tier – Nginx Web Server
Application Tier – Apache Tomcat 10
Database Tier – MySQL Server
Architecture Flow
Internet
   │
   ▼
┌─────────────────────┐
│     Web Server      │
│      Nginx          │
│  Public IP : 80     │
└──────────┬──────────┘
           │
           │ Private Network
           │ SSH : 22
           │ HTTP : 8080
           ▼
┌─────────────────────┐
│  Application Server │
│     Tomcat 10       │
│    Private IP       │
└──────────┬──────────┘
           │
           │ Private Network
           │ MySQL : 3306
           ▼
┌─────────────────────┐
│    Database Server  │
│       MySQL         │
│    Private IP       │
└─────────────────────┘
☁️ Azure Resources

The following Azure resources were created:

Resource Group
Virtual Network (VNet)
Three Subnets
Web Subnet
Application Subnet
Database Subnet
Three Virtual Machines
Web VM
Application VM
Database VM
NAT Gateway
Public IP
Network Security Rules
🖥️ Virtual Machines
Web VM
Public IP enabled
Nginx Web Server installed
SSH enabled on port 22
HTTP enabled on port 80
Application VM
Private VM
Apache Tomcat 10 installed
SSH enabled on port 22
Tomcat running on port 8080
No Public IP
Database VM
Private VM
MySQL Server installed
MySQL running on port 3306
No Public IP
Database access restricted to the Application VM

The Application and Database VMs use private networking and outbound Internet connectivity through the NAT Gateway.

🔐 Security Configuration

Security was implemented using network access rules.

Allowed Communication
Web → Application     ✅ Allowed
Application → Database ✅ Allowed
Web → Database         ❌ Restricted

The Web VM was able to communicate with the Application VM through its private IP on port 8080.

Database access was restricted so that only the Application VM could connect to MySQL. Direct Web-to-Database communication was denied.

🛠️ Technologies Used
Microsoft Azure
Azure Virtual Network
Azure Virtual Machines
Azure NAT Gateway
Network Security Groups / Inbound Rules
Linux / Ubuntu
Nginx
Apache Tomcat 10
Java OpenJDK 17
MySQL
SSH
Telnet
⚙️ Application Server Setup

Java and Tomcat were installed on the Application VM:

sudo apt update
sudo apt install -y openjdk-17-jdk
sudo apt install -y tomcat10

systemctl start tomcat10
systemctl status tomcat10
🗄️ Database Server Setup

MySQL was installed on the Database VM:

sudo apt install mysql-server -y

MySQL listening configuration was verified using:

sudo ss -lntp | grep 3306

The MySQL configuration was updated to allow the required private-network communication.

🧪 Connectivity Testing

Connectivity was tested between the different tiers using private IP addresses and Telnet.

Web → Application
Web VM → Application VM : 8080
Result: Successful ✅
Application → Database
Application VM → Database VM : 3306
Result: Successful ✅
Web → Database
Web VM → Database VM : 3306
Result: Denied ❌

This confirms that the intended three-tier security model was successfully implemented.

🎯 Project Outcome

The Azure 3-Tier Architecture was successfully implemented with:

Secure Web-to-Application communication
Secure Application-to-Database communication
Restricted direct Web-to-Database access
Private Application and Database VMs
NAT Gateway for outbound connectivity
Nginx Web Server
Tomcat Application Server
MySQL Database Server
👩‍💻 Author

Neelam Akhila

B.Tech – Electronics & Communication Engineering

Project Focus

Cloud Computing | Microsoft Azure | Networking | Linux | Nginx | Tomcat | MySQL
