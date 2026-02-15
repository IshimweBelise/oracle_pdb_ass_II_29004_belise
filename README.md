
# oracle_pdb_ass_II_29004_belise
# Oracle Pluggable Database Management Assignment

**Course:** Database Development with PL/SQL (INSY 8311)  
**Student Name:** Belise  
**Student ID:** 29004  
**Submission Date:** February 2026  
**Instructor:** Eric Maniraguha

---

## Overview

This repository contains documentation and evidence for the Oracle Pluggable Database (PDB) Management assignment. The assignment demonstrates practical understanding of Oracle Multitenant Architecture, PDB creation and deletion, user management, and Oracle Enterprise Manager usage.

---

## Oracle Environment

- **Database:** Oracle Database 21c Express Edition
- **Version:** 21.3.0.0.0
- **Platform:** Microsoft Windows x86 64-bit
- **Container Database:** XE
- **Oracle Enterprise Manager:** Database Express

---

## Tasks Completed

### Task 1: Create a New Pluggable Database

**Objective:** Create a permanent PDB with proper naming conventions and user account.

**Steps Performed:**
1. Connected to CDB as SYSDBA
2. Created PDB with name: `be_pdb_29004`
3. Opened the PDB in READ WRITE mode
4. Switched to the PDB container
5. Created user: `belise_plsqlauca_29004`
6. Granted CONNECT, RESOURCE, and DBA privileges to the user
7. Verified user creation

**Key Commands:**
```sql
-- Connect as SYSDBA
CONNECT sys AS SYSDBA;

-- Create the Pluggable Database
CREATE PLUGGABLE DATABASE be_pdb_29004
ADMIN USER pdb_admin IDENTIFIED BY 12345
CREATE_FILE_DEST = 'C:\ORACLE\ORADATA\XE';

-- Open the PDB
ALTER PLUGGABLE DATABASE be_pdb_29004 OPEN;

-- Verify PDB is open
SELECT name, open_mode FROM v$pdbs WHERE name = 'BE_PDB_29004';

-- Switch to the PDB
ALTER SESSION SET CONTAINER = be_pdb_29004;

-- Create user
CREATE USER belise_plsqlauca_29004 IDENTIFIED BY 12345;

-- Grant privileges
GRANT CONNECT, RESOURCE, DBA TO belise_plsqlauca_29004;

-- Verify user creation
SELECT username FROM dba_users WHERE username = 'BELISE_PLSQLAUCA_29004';
```

**Evidence:**
- Screenshot: PDB creation command and success message
- Screenshot: PDB in READ WRITE mode
- Screenshot: User created and verified

---

### Task 2: Create and Delete a PDB

**Objective:** Create a temporary PDB and then delete it completely.

**Steps Performed:**
1. Connected to CDB root
2. Created temporary PDB: `be_to_delete_pdb_29004`
3. Verified PDB existence
4. Dropped the PDB including all datafiles
5. Confirmed complete deletion

**Key Commands:**
```sql
-- Switch to CDB root
ALTER SESSION SET CONTAINER = CDB$ROOT;

-- Create temporary PDB
CREATE PLUGGABLE DATABASE be_to_delete_pdb_29004
ADMIN USER temp_admin IDENTIFIED BY 12345
CREATE_FILE_DEST = 'C:\ORACLE\ORADATA\XE';

-- Verify PDB exists
SELECT name, open_mode FROM v$pdbs WHERE name = 'BE_TO_DELETE_PDB_29004';

-- Drop the PDB with datafiles
DROP PLUGGABLE DATABASE be_to_delete_pdb_29004 INCLUDING DATAFILES;

-- Confirm deletion
SELECT name, open_mode FROM v$pdbs WHERE name = 'BE_TO_DELETE_PDB_29004';
-- Result: no rows selected (PDB successfully deleted)
```

**Evidence:**
<img width="416" height="82" alt="image" src="https://github.com/user-attachments/assets/a88a4e90-7c11-4b9f-805f-df2458aff444" />


- Screenshot: PDB existence verification
- Screenshot: PDB deletion command and success
- Screenshot: Deletion confirmation (no rows selected)

---

### Task 3: Oracle Enterprise Manager (OEM)

**Objective:** Access and document the Oracle Enterprise Manager dashboard.

**Steps Performed:**
1. Accessed OEM at https://localhost:5500/em
2. Logged in with SYSTEM credentials
3. Viewed Database Home dashboard
4. Verified CDB with multiple PDBs
5. Captured dashboard showing database status and resources

**Dashboard Information:**
- Database: XE (21.3.0.0.0)
- Type: Single Instance (xe)
- Container Database with multiple PDBs
- Platform: Microsoft Windows x86 64-bit
- PDB visible in Data Storage chart: BE_PDB_29004

**Evidence:**
- Screenshot: OEM Dashboard with database information and PDB visualization

---

### Task 4: Documentation & Reporting

**Repository Structure:**
```
oracle_pdb_ass_II_29004_belise/
├── README.md (this file)
└── screenshots/
    ├── task1_pdb_creation.png
    ├── task1_pdb_open.png
    ├── task1_user_created.png
    ├── task2_temp_pdb_created.png
    ├── task2_temp_pdb_exists.png
    ├── task2_pdb_deleted.png
    ├── task2_deletion_confirmed.png
    └── task3_oem_dashboard.png
```

---

## Challenges Faced and Solutions

### Challenge 1: File Path Error
**Problem:** Initial attempt to create PDB failed with ORA-65165 error due to incorrect file path.

**Solution:** 
- Queried v$datafile to identify the correct Oracle data directory path
- Discovered the correct path: `C:\ORACLE\ORADATA\XE`
- Used CREATE_FILE_DEST parameter with the correct path
- Successfully created PDB

### Challenge 2: Understanding Container Context
**Problem:** Need to ensure operations are executed in the correct container (CDB vs PDB).

**Solution:**
- Used ALTER SESSION SET CONTAINER to switch between containers
- Verified current container before executing commands
- Understood that users must be created within the PDB container

---

## Key Learnings

1. **Oracle Multitenant Architecture:** Understanding the relationship between CDB and PDBs
2. **PDB Lifecycle Management:** Creating, opening, and deleting pluggable databases
3. **Container Context:** Importance of working in the correct container for different operations
4. **User Management:** Creating users within specific PDB contexts with appropriate privileges
5. **Troubleshooting:** Resolving path issues and understanding error messages
6. **Oracle Enterprise Manager:** Using OEM for database monitoring and visualization
7. **Precision and Accuracy:** Following exact naming conventions as specified

---

## Academic Integrity Statement

I, Belise (Student ID: 29004), declare that this assignment is my original work. All commands were executed by me individually, and all screenshots are from my own Oracle Database environment. I have not copied from classmates, and I have not used AI tools to generate solutions. This work reflects my own understanding and execution of Oracle Pluggable Database management tasks.

---

## Assignment Deliverables

### PDBs Created:
- **Permanent PDB:** be_pdb_29004 (READ WRITE mode)
- **User Account:** belise_plsqlauca_29004 (with CONNECT, RESOURCE, DBA privileges)
- **Temporary PDB:** be_to_delete_pdb_29004 (created and successfully deleted)

### Screenshots Provided:
All screenshots are clearly labeled and demonstrate successful completion of each task requirement.

---

## Repository Information

- **Repository Name:** oracle_pdb_ass_II_29004_belise
- **Visibility:** Public
- **Primary PDB Created:** be_pdb_29004
- **User Created:** belise_plsqlauca_29004
- **Assignment Submission Date:** February 2026
- **GitHub URL:** [To be added after repository creation]

---

## Technical Specifications

**Oracle Database Configuration:**
- Edition: Express Edition (XE)
- Version: 21.3.0.0.0
- Data Files Location: C:\ORACLE\ORADATA\XE\
- Container Database: XE

**System Environment:**
- Operating System: Microsoft Windows x86 64-bit
- Oracle Enterprise Manager: Database Express (Port 5500)

---

## References

- Oracle Database 21c Documentation
- Oracle Multitenant Architecture Guide
- Oracle Database Administrator's Guide
- Course materials: Database Development with PL/SQL (INSY 8311)

---

**End of Documentation**
