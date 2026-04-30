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
```sh
git clone https://github.com/subhankar505s/Active-directory-webManager.git
cd Active-directory-webManager
```

### 2. Create Environment File
```sh
cp .env.example .env
```
Edit .env:
```sh
SECRET_KEY=your_random_secret_key
LDAP_DOMAIN=your.domain.com
SEARCH_DN=DC=your,DC=domain,DC=com
LDAP_SERVER=192.168.x.x
DEBUG=True
USE_LOGGING=True
ADMIN_GROUP=Domain Admins
```
### To Generate Strong SECRET_KEY
Run:
```sh
python3 -c "import secrets; print(secrets.token_hex(32))"
```
Example output:
```sh
4c9d4a0b5f2e3d6f7a8b9c0d11223344556677889900aabbccddeeff00112233
```
Paste it into:
SECRET_KEY= change_this_to_random_secret_key


### 3. Create settings.py
Create a settings.py file:
In nano:
```sh
nano settings.py
```
CTRL + K repeatedly until file empty
Then past Exactly this configuration
```sh
from decouple import config


class Settings:
    SECRET_KEY = config("SECRET_KEY")
    LDAP_DOMAIN = config("LDAP_DOMAIN")
    SEARCH_DN = config("SEARCH_DN")

    LDAP_DN = config(
        "LDAP_DN",
        default="DC=%s" % ",DC=".join(LDAP_DOMAIN.split("."))
    )

    LDAP_SERVER = config("LDAP_SERVER")
    DEBUG = config("DEBUG", cast=bool)
    USE_LOGGING = config("USE_LOGGING", cast=bool)
    SICCIP_AWARE = config("SICCIP_AWARE", default=False, cast=bool)

    ADMIN_GROUP = config("ADMIN_GROUP")

    TREE_BLACKLIST = [
        "CN=ForeignSecurityPrincipals",
        "OU=sudoers",
        "CN=Builtin",
        "CN=Infrastructure",
        "CN=LostAndFound",
        "CN=Managed Service Accounts",
        "CN=NTDS Quotas",
        "CN=Program Data",
        "CN=System",
        "OU=Domain Controllers",
        "CN=Guest",
        "CN=krbtgt"
    ]

    SEARCH_ATTRS = [
        ("sAMAccountName", "Username"),
        ("givenName", "Name")
    ]

    USER_ATTRIBUTES = [
        ["jpegPhoto", "Photo"]
    ]

    TREE_ATTRIBUTES = [
        ["mail", "Email"],
        ["__type", "Type"],
        ["active", "Status"]
    ]

```

### 4. Install Dependencies (Ubuntu/Debian)
```sh
sudo apt update
sudo apt install python3-venv python3-pip -y
sudo apt install build-essential python3-dev libldap2-dev libsasl2-dev ldap-utils tox lcov valgrind -y
```

### 5. Setup Virtual Environment
```sh
python3 -m venv ./venv
source ./venv/bin/activate
```
### 6. Install Requirements
```sh
pip install -r requirements.txt
```

## ▶️ Run the Application
```sh
python3 ADwebmanager.py
```

Open in browser:
http://localhost:8080

## 🐳 Run with Docker (Optional)
```sh
docker build -t adwebmanager .
docker run -d -p 8080:8080 adwebmanager
```
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
