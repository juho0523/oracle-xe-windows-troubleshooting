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
- Error message:
