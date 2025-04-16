

This guide walks you through installing **Apache Maven 3.9.9** on a **Red Hat Linux EC2 instance**, including Java installation, Maven setup, and environment configuration.

---

## 🛠 System Requirements

- **JDK**: 1.8 or above (Java is required before installing Maven)
- **Disk Space**: ~10MB for Maven + dependencies
- **OS**: Any Linux flavor; tested on Red Hat EC2
- **Maven Version**: 3.9.9

> 📁 All external software is installed in the `/opt` directory.

---

## 📋 Prerequisites

- Must be **logged in as root user** or use `sudo`
- Internet connection required (to download Maven and Java)

---

## 📦 Step-by-Step Installation Instructions

### ✅ Step 1: Switch to Root User

```bash
sudo su -
```

---

### ✅ Step 2: Install Java (JDK)

You can install **Java 1.8** (default) or **Java 11**:

```bash
# For JDK 1.8
sudo yum install -y java-1.8.0-openjdk-devel

# OR for Java 11
sudo yum install -y java-11-openjdk-devel
```

✅ Check the version:

```bash
java -version
javac -version
```

---

### ✅ Step 3: Prepare Environment

Install required tools and go to the `/opt` directory:

```bash
cd /opt
yum install -y wget unzip
```

---

### ✅ Step 4: Download and Extract Maven

```bash
wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.zip
unzip apache-maven-3.9.9-bin.zip
```

---

### ✅ Step 5: Set Environment Variables

Instead of updating user-specific profiles, we’ll set up a global script:

```bash
vi /etc/profile.d/maven.sh
```

Paste the following into the file:

```bash
export M2_HOME=/opt/apache-maven-3.9.9
export PATH=$PATH:$M2_HOME/bin
```

Make the script executable and apply it:

```bash
chmod +x /etc/profile.d/maven.sh
source /etc/profile.d/maven.sh
```

---

### ✅ Step 6: Verify Maven Installation

```bash
mvn -version
```

Expected output:

```
Apache Maven 3.9.9 (...)
Java version: 1.8.x or 11.x
```

---

## ⚠️ Common Errors & Fixes

| Error | Cause | Fix |
|-------|-------|-----|
| `mvn: command not found` | Environment not loaded | Run `source /etc/profile.d/maven.sh` |
| `java: command not found` | Java not installed | Install Java using yum |
| Permission denied | Not root user | Use `sudo` or switch to root |

---

## 🧠 Bonus: Make It a Script

You can automate the full process using this script:

```bash
#!/bin/bash

# Run as: sudo ./install-maven.sh

yum install -y java-1.8.0-openjdk-devel wget unzip
cd /opt
wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.zip
unzip apache-maven-3.9.9-bin.zip

echo 'export M2_HOME=/opt/apache-maven-3.9.9' > /etc/profile.d/maven.sh
echo 'export PATH=$PATH:$M2_HOME/bin' >> /etc/profile.d/maven.sh

chmod +x /etc/profile.d/maven.sh
source /etc/profile.d/maven.sh

mvn -version
```

Save this as `install-maven.sh`, make it executable (`chmod +x install-maven.sh`), and run it using `sudo`.

---

## ✅ Summary

| Task | Command |
|------|---------|
| Install Java | `yum install java-1.8.0-openjdk-devel -y` |
| Download Maven | `wget ...` |
| Unzip | `unzip apache-maven-3.9.9-bin.zip` |
| Set Env Vars | `vi /etc/profile.d/maven.sh` |
| Load Env | `source /etc/profile.d/maven.sh` |
| Verify | `mvn -version` |

---

📘 Maintained by: **KK FUNDA – DevOps & Cloud Training**  
📞 Contact: 9676831734  
🌐 Website: kkdevops.com

```

---
