# Oracle XE on Windows Troubleshooting & Docker Workaround

## 1. Overview
This repository documents the process of restoring a legacy Java web application
(Tomcat 8 + JNDI + Oracle XE) on Windows, and the issues encountered during
Oracle XE installation.

Due to multiple Windows-specific limitations (Korean user path, TEMP handling,
MSI permission errors), the final solution uses Oracle XE via Docker.

---

## 2. Environment
- OS: Windows 10 / 11
- JDK: Java 8
- WAS: Apache Tomcat 8.5
- Database: Oracle XE
- Original Project Type: Eclipse WTP Dynamic Web Project

---

## 3. Initial Goal
- Restore a legacy Eclipse-based Java web project
- Run it on Tomcat 8
- Connect to Oracle XE using JNDI DataSource

---

## 4. Issues Encountered

### 4.1 Oracle XE 21c Installation Failure (Error 1311)
- Cause: Korean characters in Windows user path
- Error message: Error 1311: Source file not found ...

  
### 4.2 TEMP Directory Workaround and Side Effect (Error 2503)
- TEMP/TMP changed to `C:\temp`
- New issue:Error 2503: Called RunScript when not marked in progress

  - Root cause: MSI installer permission issues on custom TEMP directory

---

## 5. Attempted Solutions
- Change Oracle installation directory to English path
- Override TEMP/TMP environment variables
- Run installer as Administrator
- Downgrade Oracle XE version (21c → 11g)
- Re-register Windows Installer

> Result: Windows-native Oracle XE installation remained unstable.

---

## 6. Final Solution: Oracle XE with Docker

### 6.1 Why Docker
- Avoid Windows MSI installer issues
- Avoid Korean path encoding problems
- Easy cleanup and reproducibility

### 6.2 Docker Command
```bash
docker run -d \
--name oracle-xe \
-p 1521:1521 \
-e ORACLE_PASSWORD=hr1 \
gvenzl/oracle-xe:11

