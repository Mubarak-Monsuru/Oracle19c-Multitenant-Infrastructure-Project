# Project 1: Cross-Platform Multitenant Infrastructure, Enterprise Security & Data Pipelines

## 1. Overview & Architecture
* **Client / Admin Node:** Windows Workstation (Remote Administrative Endpoint)
* **Database Server Node:** Oracle Linux 19c Server (Host for CDB & PDBs)
* **Architecture Model:** $\text{Windows Client (Admin/Dev)} \iff \text{Oracle Linux 19c Server (CDB/PDBs)}$

### Scenario & Workflow
This project involves deploying a multi-tier enterprise database architecture. The core database infrastructure (Container Database `oradb_cdb` and Pluggable Databases `pdb1`, `pdb2`) resides on the Oracle Linux 19c server. Administrative tasks, security policy enforcement, data ingestion pipelines, and reporting operations are executed remotely from the Windows workstation using SQL*Plus, SQL Developer, SQL*Loader, and Data Pump.

---

## 2. Core Objectives
* Design and establish secure cross-platform connectivity between a Windows workstation and an Oracle Linux 19c server.
* Provision and configure Oracle 19c Container (CDB) and Pluggable Databases (PDBs) along with automatic storage and memory tuning (ASMM).
* Implement administrative lifecycle workflows for multitenant databases entirely from a remote client.
* Enforce enterprise security standards using common/local users, roles, password profiles, and secure authentication models.
* Build remote data pipelines using SQL*Loader, External Tables, and Data Pump across network links.
* Automate recurring database maintenance and statistics collection using `DBMS_SCHEDULER`.

---

## 3. Project Tasks Breakdown

### Phase 1: Database Creation, Storage & Memory Architecture (1Z0-082)
- [ ] Install Oracle Database 19c software on Oracle Linux 19c server.
- [ ] Create Container Database (`oradb_cdb`) and initial Pluggable Databases (`pdb1`, `pdb2`) using DBCA and SQL scripts.
- [ ] Configure Automatic Shared Memory Management (ASMM), tuning `SGA_TARGET` and `PGA_AGGREGATE_TARGET` parameters.
- [ ] Provision `BIGFILE` tablespaces, manage datafiles, and configure undo segments for multitenant isolation.

### Phase 2: Cross-Platform Networking & Connectivity Setup (1Z0-082)
- [ ] Configure `listener.ora` on Oracle Linux to listen on port `1521` and accept external client requests.
- [ ] Configure `tnsnames.ora` and `sqlnet.ora` on the Windows Workstation to map network descriptors to `oradb_cdb`, `pdb1`, and `pdb2`.
- [ ] Configure Shared Server dispatchers on the Oracle Linux host.
- [ ] Verify cross-platform connectivity from Windows using both SQL*Plus and SQL Developer.
- [ ] Establish Database Links (`DBLINK`) between PDBs and execute remote cross-PDB queries.

### Phase 3: Multitenant Lifecycle Operations (1Z0-082 & 1Z0-083)
- [ ] Perform remote PDB lifecycle operations from the Windows workstation:
  - [ ] Hot and cold cloning of `pdb1` into new test PDBs.
  - [ ] Unplugging a PDB to a `.pdb` / `.xml` manifest and plugging it into the CDB.
  - [ ] Dropping PDBs safely with datafiles.
  - [ ] Managing startup/shutdown states and setting `AUTOSTART` policies for PDBs.

### Phase 4: Enterprise Security & Remote Authentication (1Z0-082)
- [ ] Implement Common Users (e.g., `C##admin`) and assign Common Roles across all PDBs.
- [ ] Create Local Users and assign granular Local Roles within specific PDBs.
- [ ] Design and enforce Password Profiles (failed login attempts, password lifetime, complexity rules).
- [ ] Configure Remote Password File authentication (`orapwd`) to allow secure remote `SYSDBA` access from Windows.
- [ ] Test and document OS-based authentication vs. password file authentication.

### Phase 5: Remote Data Ingestion & Data Pipelines (1Z0-082)
- [ ] Prepare flat CSV data files on the Windows client workstation.
- [ ] Execute remote `SQLLDR` (SQL*Loader) from Windows to ingest data into target PDB tables.
- [ ] Define Oracle External Tables over staging files on the server for direct querying.
- [ ] Perform remote Data Pump exports (`expdp`) and imports (`impdp`) over Network Links between PDBs.

### Phase 6: Automated Task Scheduling & Maintenance (1Z0-082)
- [ ] Create custom database jobs using `DBMS_SCHEDULER` to automate optimizer statistics gathering (`DBMS_STATS`).
- [ ] Configure automated maintenance windows and schedule log/purge routines.
- [ ] Verify job execution logs and monitor status via `DBA_SCHEDULER_JOBS` views.