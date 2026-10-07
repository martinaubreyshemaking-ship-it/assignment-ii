# assignment-ii
-- 1. Create the PDB (the admin user doubles as your required username)
CREATE PLUGGABLE DATABASE au_pdb_<ID>
  ADMIN USER aubrey_plsqlauca_<ID> IDENTIFIED BY Oracle123
  FILE_NAME_CONVERT = ('/pdbseed/', '/au_pdb_<ID>/');

-- 2. Open it and make it auto-open on restart
ALTER PLUGGABLE DATABASE au_pdb_<ID> OPEN;
ALTER PLUGGABLE DATABASE au_pdb_<ID> SAVE STATE;

-- 3. Switch into it and give the user rights
ALTER SESSION SET CONTAINER = au_pdb_<ID>;
GRANT CONNECT, RESOURCE, DBA TO aubrey_plsqlauca_<ID>;

-- 4. Verify (screenshot these for your docs)
SHOW CON_NAME;
SELECT name, open_mode FROM v$pdbs;
-- 0. Go back to the root
ALTER SESSION SET CONTAINER = CDB$ROOT;
SHOW CON_NAME;

-- 1. CREATE the temp PDB
CREATE PLUGGABLE DATABASE au_to_delete_pdb_<ID>
  ADMIN USER tempadmin IDENTIFIED BY Oracle123
  FILE_NAME_CONVERT = ('/pdbseed/', '/au_to_delete_pdb_<ID>/');

ALTER PLUGGABLE DATABASE au_to_delete_pdb_<ID> OPEN;

-- 2. VERIFY it exists  (screenshot 1: command + result)
SELECT name, open_mode FROM v$pdbs;

-- 3. DELETE it completely  (screenshot 2: command + result)
ALTER PLUGGABLE DATABASE au_to_delete_pdb_<ID> CLOSE IMMEDIATE;
DROP PLUGGABLE DATABASE au_to_delete_pdb_<ID> INCLUDING DATAFILES;

-- 4. CONFIRM it's gone
SELECT name, open_mode FROM v$pdbs;
<img width="661" height="573" alt="image" src="https://github.com/user-attachments/assets/33c79d28-1e02-4a77-957f-4d14643175f3" />
mkdir oracle_pdb_ass_II_<ID>_aubrey && cd oracle_pdb_ass_II_<ID>_aubrey
mkdir -p screenshots/pdb_creation screenshots/pdb_deletion screenshots/oem_dashboard
# drop your screenshots into those 3 folders (git ignores empty folders)
# Oracle PDB Assignment II

## Overview of Tasks
| # | Task | Type |
|---|------|------|
| 1 | Create a New Pluggable Database | Technical |
| 2 | Create and Delete a PDB | Technical |
| 3 | Oracle Enterprise Manager (OEM) Setup | Technical |
| 4 | Documentation & Reporting | Documentation |

## Oracle Environment Used
- Oracle Database version: <e.g. 19c / 21c>
- OS: <e.g. Windows 11 / Oracle Linux>
- Tools: SQL*Plus / SQL Developer, Oracle Enterprise Manager

## Explanation of Each Task

### Task 1: Create a New Pluggable Database
Created the PDB `au_pdb_<ID>` from the seed with admin user `aubrey_plsqlauca_<ID>`, opened it, saved its state, and granted the user the required privileges. Verified with `SHOW CON_NAME` and `v$pdbs`.
Screenshots: `screenshots/pdb_creation/`

### Task 2: Create and Delete a PDB
Created the temporary PDB `au_to_delete_pdb_<ID>`, confirmed it existed in `v$pdbs`, closed it, dropped it with `INCLUDING DATAFILES`, and confirmed it no longer appears.
Screenshots: `screenshots/pdb_deletion/`

### Task 3: OEM Setup
<briefly describe how you set up / accessed OEM and what the dashboard shows>
Screenshots: `screenshots/oem_dashboard/`

### Task 4: Documentation & Reporting
Documented all steps in this README and published the evidence on public GitHub.

## Challenges Faced and Solutions
- <challenge 1> → <how you fixed it>
- (If none, write: No major issues encountered.)

## Integrity Statement
I confirm that this work is my own, that all screenshots were taken from my own environment, and that I have not copied the work of others.

## Submission Details
Repository Link: https://github.com/<your-username>/oracle_pdb_ass_II_<ID>_aubrey
PDB Name Created: au_pdb_<ID>
Issues Encountered: <Yes/No>
git init
git add .
git commit -m "Oracle PDB Assignment II"
git branch -M main
git remote add origin https://github.com/<your-username>/oracle_pdb_ass_II_<ID>_aubrey.git
git push -u origin main
