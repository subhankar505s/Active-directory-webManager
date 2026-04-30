# Active-directory-webManager
A web-based administrative portal for managing Enterprise Active Directory using Samba 4, LDAP, and Flask. It enables user creation, password reset, group management, authentication, and audit logging through a secure and intuitive browser interface, reducing dependency on command-line tools

# 🛠️ AD Web Manager
Web-Based Administrative Portal for Active Directory

## 📌 Description
This project is a web-based interface for managing Active Directory using Flask and python-ldap. It provides a simple and intuitive way to perform common directory operations such as user management, password reset, and group administration without relying on command-line tools or Windows interfaces. It uses the connecting user's credentials to interact with the directory and supports both Windows Active Directory and Samba4 domain controllers.

## 🚀 Features
- User creation and deletion
- Password reset
- Group management
- LDAP search operations
- Authentication using directory credentials
- Audit logging
- Compatible with Windows AD and Samba4

## 🏗️ Tech Stack
- Backend: Flask (Python)
- Directory Access: python-ldap
- Protocols: LDAP, Kerberos
- Environment: Linux

## 📜 Project Background
This project started as a fork of samba4-manager, created by Stéphane Graber and the Edubuntu community. It was used internally at Havana's Technology University in 2017 and later extended with numerous updates and improvements. The project is now maintained by GSI General Software Inc. and continues to evolve with community contributions.

## ⚙️ System Requirements
- Linux (Ubuntu/Debian recommended)
- Python 3.x
- LDAP Server (Samba4 / Windows AD)
- Domain Controller access

## 🔧 Installation & Setup

### 1. Clone the Repository
git clone https://github.com/subhankar505s/Active-directory-webManager.git
cd Active-directory-webManager

### 2. Create Environment File

cp .env.example .env

* Create the .env file in the root directory
  * Put a random string in SECRET\_KEY**
  * Set LDAP\_DOMAIN to your Directory domain
  * Set SEARCH\_DN to your Directory LDAP search base
  * Set LDAP\_SERVER to your Domain Controller IP
  * Use DEBUG = True if you want the test server to immediately reload after changes
  * Set USE_LOGGING = True if you want to log to files and console, false logs to console only
  * Set ADMIN\_GROUP to the security group with read/write permission (default should be Domain Admins)
* Create settings.py to configure**
* ADD to TREE\_BLACKLIST the containers you want to hide in the root directory
* Add attribute pairs to SEARCH\_ATTRS and TREE\_ATTRIBUTES to customize the tree view


### 3. Create settings.py
Create a settings.py file:
TREE_BLACKLIST = []
SEARCH_ATTRS = []
TREE_ATTRIBUTES = []

### 4. Install Dependencies (Ubuntu/Debian)
sudo apt update
sudo apt install python3-venv python3-pip -y
sudo apt install build-essential python3-dev libldap2-dev libsasl2-dev ldap-utils tox lcov valgrind -y

### 5. Setup Virtual Environment
python3 -m venv ./venv
source ./venv/bin/activate

### 6. Install Requirements
pip install -r requirements.txt

## ▶️ Run the Application
python3 ADwebmanager.py

Open in browser:
http://localhost:8080

## 🐳 Run with Docker (Optional)
docker build -t adwebmanager .
docker run -d -p 8080:8080 adwebmanager

Access:
http://localhost:8080

## 🔐 Configuration Notes
- Uses user credentials for LDAP binding
- Admin access controlled via ADMIN_GROUP
- Logging configurable via .env

## 🧪 Development Mode
Set DEBUG=True in .env for auto reload

## 🤝 Contributing
Contributions are always appreciated!
1. Fork the repository
2. Create a new branch
3. Commit your changes
4. Push to GitHub
5. Open a Pull Request

## 📄 License
This project is licensed under the MIT License

## ⭐ Final Note
This project simplifies enterprise Active Directory management by providing a secure, scalable, and user-friendly web-based alternative to traditional command-line and Windows-based tools.
