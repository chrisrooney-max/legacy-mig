# WST Application Analysis

<!-- Input files processed:
- src/defra-wst/src/WST.sln
- src/defra-wst/src/WST/WST.vbproj
- src/defra-wst/src/WST/Web.config
- src/defra-wst/src/WST/Web.sitemap
- src/defra-wst/src/WST/Common.vb
- src/defra-wst/src/WST/MasterPage.Master
- src/defra-wst/src/WST/MasterPage.Master.vb
- src/defra-wst/src/WST/Default.aspx
- src/defra-wst/src/WST/Default.aspx.vb
- src/defra-wst/src/WST/WSTHome.aspx
- src/defra-wst/src/WST/WSTHome.aspx.vb
- src/defra-wst/src/WST/Help.aspx
- src/defra-wst/src/WST/Help.aspx.vb
- src/defra-wst/src/WST/Auditlog.aspx
- src/defra-wst/src/WST/Auditlog.aspx.vb
-->

## 1. Application Overview

**Purpose:** Workplace Safety Training Certification Database for managing safety training records, certifications, personnel, instructors, and facilities within NSA operations.

**Technology stack:** VB.NET, ASP.NET Web Forms, .NET Framework

**Framework version:** .NET Framework 4.8

**Solution structure:**
- WST (single web application project)

**External dependencies:**
- ClosedXML.0.95.4 (Excel generation library)
- DocumentFormat.OpenXml.2.7.2 (Excel support)
- ExcelNumberFormat.1.0.10 (Excel number formatting)

**Configuration summary:**
- Windows Authentication enabled
- SQL Server database connection to WSTSQL01
- File upload path configured to "Files/"
- Custom error pages for 404 (FileNotFound.aspx) and 403 (UnauthorisedAccess.aspx)
- Debug mode enabled, compilation set to non-strict

## 2. User Roles and Access Control

| Role | Permissions / Access | Source |
|------|---------------------|--------|
| Superuser (Level 1) | Full access to all functions including user management, news management, and all CRUD operations | src/defra-wst/src/WST/MasterPage.Master.vb, src/defra-wst/src/WST/WSTHome.aspx.vb |
| Data entry (Level 2) | Can add, edit, delete persons, instructors, facilities, certifications; cannot manage users or news | src/defra-wst/src/WST/MasterPage.Master.vb, src/defra-wst/src/WST/WSTHome.aspx.vb |
| Read only (Level 3) | View-only access to all data; all input controls disabled | src/defra-wst/src/WST/MasterPage.Master.vb, src/defra-wst/src/WST/WSTHome.aspx.vb |

**Authentication mechanism:** Windows Authentication with impersonation disabled

**Authorisation approach:** Database-driven role checks combined with per-page authorisation controls via stored procedure `sp_DataEntry_Get` that determines write permissions based on user level and active view

## 3. Features and Capabilities

#### Personnel Management
- **Description:** Manage safety training candidates/personnel at various facilities
- **Pages/screens:** WSTHome.aspx views 1, 3, 4 (Add Person, Edit Person, View People)
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx, src/defra-wst/src/WST/WSTHome.aspx.vb

#### Instructor Management
- **Description:** Manage safety training instructors and their regional office assignments
- **Pages/screens:** WSTHome.aspx views 5, 7, 8 (Add Instructor, Edit Instructor, Instructor History)
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx, src/defra-wst/src/WST/WSTHome.aspx.vb

#### Certification Management
- **Description:** Record and manage safety certifications for chemical, electrical, and mechanical hazard types
- **Pages/screens:** WSTHome.aspx views 9, 11, 12 (Add Certification, Edit Certification, View Certifications)
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx, src/defra-wst/src/WST/WSTHome.aspx.vb

#### Facility Management
- **Description:** Manage facility records including contact details and personnel assignments
- **Pages/screens:** WSTHome.aspx views 13, 15, 16, 22 (Add Facility, Edit Facility, View Facilities, Facility Personnel)
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx, src/defra-wst/src/WST/WSTHome.aspx.vb

#### User Administration
- **Description:** Manage system users with domain accounts and permission levels
- **Pages/screens:** WSTHome.aspx views 17, 19, 20 (Add User, Edit User, View Users)
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx, src/defra-wst/src/WST/WSTHome.aspx.vb

#### Regional Office Management
- **Description:** Manage regional offices and their instructor assignments
- **Pages/screens:** WSTHome.aspx views 10, 21, 23 (Add Regional Office, View Regional Offices, Office Instructors)
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx, src/defra-wst/src/WST/WSTHome.aspx.vb

#### News Management
- **Description:** Publish and manage news items displayed on the home page
- **Pages/screens:** WSTHome.aspx views 14, 18 (Add News, View/Delete News)
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx, src/defra-wst/src/WST/WSTHome.aspx.vb

#### Reporting
- **Description:** Generate comprehensive Excel reports with all system data
- **Pages/screens:** WSTHome.aspx view 25 (Export Report)
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx, src/defra-wst/src/WST/WSTHome.aspx.vb

#### Audit Logging
- **Description:** View and archive audit trails of system operations
- **Pages/screens:** Auditlog.aspx, AuditLogArchive.aspx
- **Source files:** src/defra-wst/src/WST/Auditlog.aspx, src/defra-wst/src/WST/Auditlog.aspx.vb

#### Help System
- **Description:** Context-sensitive help with screenshots for each functional area
- **Pages/screens:** Help.aspx with multiple views
- **Source files:** src/defra-wst/src/WST/Help.aspx, src/defra-wst/src/WST/Help.aspx.vb

## 4. Workflows and Behaviours

#### Personnel Registration Workflow
- **Type:** user-facing
- **Trigger:** User selects "Add a person" from Person menu
- **Steps:**
  1. User enters person's name (surname, first name format) — src/defra-wst/src/WST/WSTHome.aspx
  2. User selects facility from dropdown list — src/defra-wst/src/WST/WSTHome.aspx
  3. System validates required fields — src/defra-wst/src/WST/WSTHome.aspx.vb
  4. System calls `sp_Candidate_Add` stored procedure — src/defra-wst/src/WST/WSTHome.aspx.vb
  5. System logs audit trail via Common.DataWriter — src/defra-wst/src/WST/Common.vb
  6. Success message displayed and form reset — src/defra-wst/src/WST/WSTHome.aspx.vb
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx, src/defra-wst/src/WST/WSTHome.aspx.vb, src/defra-wst/src/WST/Common.vb

#### Certification Assignment Workflow
- **Type:** user-facing
- **Trigger:** User selects "Add certification" from Certification menu
- **Steps:**
  1. User selects candidate from dropdown — src/defra-wst/src/WST/WSTHome.aspx
  2. User selects instructor from dropdown — src/defra-wst/src/WST/WSTHome.aspx
  3. User selects certification level (Peer-Certified, Certified, Recertified) — src/defra-wst/src/WST/WSTHome.aspx
  4. User enters/selects certification date via calendar control — src/defra-wst/src/WST/WSTHome.aspx
  5. User selects hazard type (Chemical, Electrical, Mechanical) — src/defra-wst/src/WST/WSTHome.aspx
  6. System validates all fields are completed — src/defra-wst/src/WST/WSTHome.aspx.vb
  7. System checks for duplicate certification via `sp_Certification_Add` — src/defra-wst/src/WST/WSTHome.aspx.vb
  8. If successful, records certification and resets form — src/defra-wst/src/WST/WSTHome.aspx.vb
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx, src/defra-wst/src/WST/WSTHome.aspx.vb

#### User Authentication and Authorisation Workflow
- **Type:** system/background
- **Trigger:** Page load on any protected page
- **Steps:**
  1. Master page loads and retrieves Windows identity — src/defra-wst/src/WST/MasterPage.Master.vb
  2. System queries `sp_User_Get` with Windows identity — src/defra-wst/src/WST/MasterPage.Master.vb
  3. If user not found, redirect to Unauthorised.htm — src/defra-wst/src/WST/MasterPage.Master.vb
  4. If found, set session UserLevel and display role — src/defra-wst/src/WST/MasterPage.Master.vb
  5. On main page, check per-view permissions via `sp_DataEntry_Get` — src/defra-wst/src/WST/WSTHome.aspx.vb
  6. Disable controls based on user level and view permissions — src/defra-wst/src/WST/WSTHome.aspx.vb
- **Source files:** src/defra-wst/src/WST/MasterPage.Master.vb, src/defra-wst/src/WST/WSTHome.aspx.vb

#### Excel Report Generation Workflow
- **Type:** user-facing
- **Trigger:** User clicks Excel export button in Reports section
- **Steps:**
  1. System executes 5 report stored procedures for different data sets — src/defra-wst/src/WST/WSTHome.aspx.vb
  2. System loads Excel template from ~/Reports/WST.xlsx — src/defra-wst/src/WST/WSTHome.aspx.vb
  3. System populates 5 worksheets with data from stored procedures — src/defra-wst/src/WST/WSTHome.aspx.vb
  4. System adds hyperlinks between related data — src/defra-wst/src/WST/WSTHome.aspx.vb
  5. System saves file to configured folder path — src/defra-wst/src/WST/WSTHome.aspx.vb
  6. System sends file to browser as download — src/defra-wst/src/WST/WSTHome.aspx.vb
- **Source files:** src/defra-wst/src/WST/WSTHome.aspx.vb

#### Audit Logging Workflow
- **Type:** system/background
- **Trigger:** Any database write operation via Common.DataWriter
- **Steps:**
  1. DataWriter method executes specified stored procedure — src/defra-wst/src/WST/Common.vb
  2. If not excluded procedure (sp_Audit_log_DELETE, sp_Usage_Insert), log audit — src/defra-wst/src/WST/Common.vb
  3. System serialises parameters to string format — src/defra-wst/src/WST/Common.vb
  4. System gets current Windows user identity — src/defra-wst/src/WST/Common.vb
  5. System calls `sp_Audit_Log` with procedure, parameters, user, and type — src/defra-wst/src/WST/Common.vb
- **Source files:** src/defra-wst/src/WST/Common.vb

## 5. Business Rules and Validation

| ID | Rule | Description | Criticality | Source |
|------|------|-------------|-------------|--------|
| BR-001 | Unique Person-Facility Assignment | A person can only be registered once per facility | Core | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-002 | Unique Certification per Hazard Type | A candidate cannot have duplicate certifications for the same hazard type | Core | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-003 | Facility Code Uniqueness | Facility codes must be unique across the system | Core | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-004 | Required Person Name Format | Person names must be entered in "surname, first name" format | Supporting | src/defra-wst/src/WST/WSTHome.aspx |
| BR-005 | Facility Assignment Required | Persons must be assigned to a facility upon registration | Supporting | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-006 | Regional Office Assignment Required | Instructors must be assigned to a regional office | Supporting | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-007 | Certification Date Validation | Certification dates must be valid dates in DD/MM/YYYY format | Supporting | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-008 | Deletion Cascade Protection | Persons with certification records cannot be deleted | Core | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-009 | Instructor Deletion Protection | Instructors who have given certifications cannot be deleted | Core | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-010 | Facility Deletion Protection | Facilities with assigned personnel cannot be deleted | Core | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-011 | Regional Office Deletion Protection | Regional offices with assigned instructors cannot be deleted | Core | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-012 | User Domain Format | User IDs must follow domain format (default NSADOM\) | Supporting | src/defra-wst/src/WST/WSTHome.aspx |
| BR-013 | Numeric Office ID Validation | Regional office IDs must be numeric values | Supporting | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-014 | Hazard Type Enumeration | Certifications limited to Chemical, Electrical, or Mechanical hazard types | Supporting | src/defra-wst/src/WST/WSTHome.aspx |
| BR-015 | Certification Level Enumeration | Certification levels limited to Peer-Certified, Certified, or Recertified | Supporting | src/defra-wst/src/WST/WSTHome.aspx |
| BR-016 | User Level Enumeration | User access levels limited to 1 (Superuser), 2 (Data entry), or 3 (Read only) | Core | src/defra-wst/src/WST/MasterPage.Master.vb |
| BR-017 | Windows Authentication Required | All users must authenticate via Windows domain accounts | Core | src/defra-wst/src/WST/MasterPage.Master.vb |
| BR-018 | Authorised User Registration | Only registered users in the database can access the system | Core | src/defra-wst/src/WST/MasterPage.Master.vb |
| BR-019 | Role-Based Function Access | Superusers only can manage users and news; Data entry excluded from some views | Core | src/defra-wst/src/WST/WSTHome.aspx.vb |
| BR-020 | Audit Trail Mandatory | All write operations except excluded procedures must be logged | Core | src/defra-wst/src/WST/Common.vb |

## 6. Domain Model

#### Person (Candidate/Trainee)
- **Purpose:** Represents individuals who receive safety training certifications
- **Source file:** src/defra-wst/src/WST/WSTHome.aspx.vb

| Property | Type | Description | Source |
|----------|------|-------------|--------|
| Candidate_No | Integer | Primary key identifier | src/defra-wst/src/WST/WSTHome.aspx |
| CandidateName | String | Person's name in surname, first name format | src/defra-wst/src/WST/WSTHome.aspx |
| Facility_Code | String | Associated facility code | src/defra-wst/src/WST/WSTHome.aspx |

#### Instructor (Trainer)
- **Purpose:** Represents individuals authorised to provide safety training certifications
- **Source file:** src/defra-wst/src/WST/WSTHome.aspx.vb

| Property | Type | Description | Source |
|----------|------|-------------|--------|
| Instructor_ID | Integer | Primary key identifier | src/defra-wst/src/WST/WSTHome.aspx |
| InstructorName | String | Instructor's name | src/defra-wst/src/WST/WSTHome.aspx |
| Office_ID | Integer | Associated regional office ID | src/defra-wst/src/WST/WSTHome.aspx |

#### Facility
- **Purpose:** Represents physical locations where personnel are assigned
- **Source file:** src/defra-wst/src/WST/WSTHome.aspx.vb

| Property | Type | Description | Source |
|----------|------|-------------|--------|
| Facility_Code | String | Primary key facility identifier | src/defra-wst/src/WST/WSTHome.aspx |
| Name | String | Facility name | src/defra-wst/src/WST/WSTHome.aspx |
| Address_Line1 | String | First line of address | src/defra-wst/src/WST/WSTHome.aspx |
| Address_Line2 | String | Second line of address | src/defra-wst/src/WST/WSTHome.aspx |
| Address_Town | String | Town | src/defra-wst/src/WST/WSTHome.aspx |
| Address_County | String | County | src/defra-wst/src/WST/WSTHome.aspx |
| Address_PostCode | String | Postal code | src/defra-wst/src/WST/WSTHome.aspx |
| Telephone | String | Phone number | src/defra-wst/src/WST/WSTHome.aspx |
| Fax | String | Fax number | src/defra-wst/src/WST/WSTHome.aspx |
| IsNSAOffice | Boolean | Whether this is an NSA office | src/defra-wst/src/WST/WSTHome.aspx.vb |

#### Certification
- **Purpose:** Represents a safety training certification record
- **Source file:** src/defra-wst/src/WST/WSTHome.aspx.vb

| Property | Type | Description | Source |
|----------|------|-------------|--------|
| Candidate_No | Integer | Foreign key to person | src/defra-wst/src/WST/WSTHome.aspx |
| Instructor_ID | Integer | Foreign key to instructor | src/defra-wst/src/WST/WSTHome.aspx |
| Date_Certified | DateTime | Date of certification | src/defra-wst/src/WST/WSTHome.aspx |
| Hazard_Type | String | Type of hazard (Chemical/Electrical/Mechanical) | src/defra-wst/src/WST/WSTHome.aspx |
| CertLevel | String | Certification level | src/defra-wst/src/WST/WSTHome.aspx |

#### RegionalOffice
- **Purpose:** Represents regional offices where instructors are based
- **Source file:** src/defra-wst/src/WST/WSTHome.aspx.vb

| Property | Type | Description | Source |
|----------|------|-------------|--------|
| Office_ID | Integer | Primary key office identifier | src/defra-wst/src/WST/WSTHome.aspx |
| Office_Name | String | Office name | src/defra-wst/src/WST/WSTHome.aspx |

#### User
- **Purpose:** Represents system users with access permissions
- **Source file:** src/defra-wst/src/WST/WSTHome.aspx.vb

| Property | Type | Description | Source |
|----------|------|-------------|--------|
| UserID | String | Windows domain account identifier | src/defra-wst/src/WST/WSTHome.aspx |
| UserName | String | Display name | src/defra-wst/src/WST/WSTHome.aspx |
| User_Office | Integer | Associated regional office | src/defra-wst/src/WST/WSTHome.aspx |
| UserLevel | Integer | Permission level (1=Superuser, 2=Data entry, 3=Read only) | src/defra-wst/src/WST/WSTHome.aspx |

#### News
- **Purpose:** Represents news items displayed on the home page
- **Source file:** src/defra-wst/src/WST/WSTHome.aspx.vb

| Property | Type | Description | Source |
|----------|------|-------------|--------|
| Title | String | News title | src/defra-wst/src/WST/WSTHome.aspx |
| NewsContent | String | News content body | src/defra-wst/src/WST/WSTHome.aspx |
| DatePublished | DateTime | Publication date | src/defra-wst/src/WST/WSTHome.aspx |
| Author | String | News author | src/defra-wst/src/WST/WSTHome.aspx |

#### Enumerations

| Enum Name | Values | Source |
|-----------|--------|--------|
| HazardType | Chemical, Electrical, Mechanical | src/defra-wst/src/WST/WSTHome.aspx |
| CertificationLevel | Peer-Certified, Certified, Recertified | src/defra-wst/src/WST/WSTHome.aspx |
| UserLevel | 1 (Superuser), 2 (Data entry), 3 (Read only) | src/defra-wst/src/WST/MasterPage.Master.vb |

#### Relationships

| Entity A | Entity B | Relationship Type | Source |
|----------|----------|-------------------|--------|
| Person | Facility | Many-to-One (Person belongs to Facility) | src/defra-wst/src/WST/WSTHome.aspx |
| Instructor | RegionalOffice | Many-to-One (Instructor belongs to RegionalOffice) | src/defra-wst/src/WST/WSTHome.aspx |
| Certification | Person | Many-to-One (Certification belongs to Person) | src/defra-wst/src/WST/WSTHome.aspx |
| Certification | Instructor | Many-to-One (Certification given by Instructor) | src/defra-wst/src/WST/WSTHome.aspx |
| User | RegionalOffice | Many-to-One (User belongs to RegionalOffice) | src/defra-wst/src/WST/WSTHome.aspx |

## 7. Integration Points

| Integration | Type | Endpoint / Target | Direction | Source |
|-------------|------|-------------------|-----------|--------|
| Email Notifications | email | wst-system@nsa.example.com / support@nsa.example.com | outbound | src/defra-wst/src/WST/Common.vb |
| SMTP Server | email | mail.nsa-internal.example.com | outbound | src/defra-wst/src/WST/Common.vb |
| File System | file I/O | Files/ folder (configurable path) | bidirectional | src/defra-wst/src/WST/WSTHome.aspx.vb |
| Excel Template | file I/O | ~/Reports/WST.xlsx | inbound | src/defra-wst/src/WST/WSTHome.aspx.vb |
| Windows Domain | external system | NSADOM\ (Windows Authentication) | inbound | src/defra-wst/src/WST/MasterPage.Master.vb |

## 8. Reports

| Report | Type | Purpose | Data Sources | Parameters | Output Format | Source |
|--------|------|---------|-------------|------------|---------------|--------|
| Comprehensive Export | code-generated | Export all system data to Excel workbook | sp_Report_Facility, sp_Report_Candidate, sp_Report_Instructor, sp_Report_Certification, sp_Report_NSA | None | Excel (.xlsx) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| Audit Log | code-generated | Display audit trail of system operations | sp_Audit_log_Get | Stored procedure filter | HTML GridView | src/defra-wst/src/WST/Auditlog.aspx.vb |
| Audit Log Archive | code-generated | Display archived audit records | Database tables | None | HTML GridView | src/defra-wst/src/WST/AuditLogArchive.aspx |

## 9. Cross-Reference: Application to Database

#### 9.1 Data Access Patterns

**Primary data access approach:** ADO.NET with SqlConnection, SqlCommand, and SqlDataAdapter; Custom Common class wraps database operations with automatic audit logging

#### 9.2 Entity-to-Table Mapping

| Entity / Class | Database Table(s) | Source |
|---------------|-------------------|--------|
| Person/Candidate | tblCandidates (inferred from stored procedures) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| Instructor | tblInstructors | src/defra-wst/src/WST/WSTHome.aspx |
| Facility | tblFacilities (inferred from stored procedures) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| Certification | tblCertifications (inferred from stored procedures) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| RegionalOffice | tblRegionalOffices (inferred from stored procedures) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| User | tblUsers (inferred from stored procedures) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| News | tblNews (inferred from stored procedures) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| AuditLog | tblAuditLog (inferred from stored procedures) | src/defra-wst/src/WST/Common.vb |

#### 9.3 Stored Procedure Calls

| Stored Procedure | Calling File(s) | Purpose | Source |
|-----------------|-----------------|---------|--------|
| sp_Candidate_Add | WSTHome.aspx.vb | Add new person/candidate | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Candidate_Update | WSTHome.aspx.vb | Update person details | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Candidate_Delete | WSTHome.aspx.vb | Delete person (with cascade check) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Candidate_Select | WSTHome.aspx.vb | Retrieve person/candidate data | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Instructor_Add | WSTHome.aspx.vb | Add new instructor | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Instructor_Update | WSTHome.aspx.vb | Update instructor details | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Instructor_Delete | WSTHome.aspx.vb | Delete instructor (with cascade check) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Instructor_CertifiedBy_Certified | WSTHome.aspx.vb | Get instructor certification history | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Instructor_ShowAllCertifications_Select | WSTHome.aspx.vb | Get all certifications by instructor | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Facility_Add | WSTHome.aspx.vb | Add new facility | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Facility_Update | WSTHome.aspx.vb | Update facility details | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Facility_Delete | WSTHome.aspx.vb | Delete facility (with cascade check) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Facility_Select | WSTHome.aspx.vb | Retrieve facility data | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Facility_View | WSTHome.aspx.vb | View facility details | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_FacilityPersonnel_Select | WSTHome.aspx.vb | Get personnel by facility | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Certification_Add | WSTHome.aspx.vb | Add new certification | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Certification_Update | WSTHome.aspx.vb | Update certification record | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Certification_Delete | WSTHome.aspx.vb | Delete certification | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Certification_View | WSTHome.aspx.vb | View certifications by candidate | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_RegionalOffice_Add | WSTHome.aspx.vb | Add new regional office | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_RegionalOffice_Delete | WSTHome.aspx.vb | Delete regional office (with cascade check) | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_RegionalOffice_Select | WSTHome.aspx.vb | Retrieve regional office data | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_RegionalOffice_Instructors | WSTHome.aspx.vb | Get instructors by office | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_User_Add | WSTHome.aspx.vb | Add new user | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_User_Update | WSTHome.aspx.vb | Update user details | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_User_Delete | WSTHome.aspx.vb | Delete user | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_User_Get | MasterPage.Master.vb | Get user details by Windows identity | src/defra-wst/src/WST/MasterPage.Master.vb |
| sp_User_Select | WSTHome.aspx.vb | Retrieve user data | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_News_Add | WSTHome.aspx.vb | Add news item | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_News_Delete | WSTHome.aspx.vb | Delete news item | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_GetNews | WSTHome.aspx.vb | Get recent news items | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_GetAllNews | WSTHome.aspx.vb | Get all news items | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_DataEntry_Get | WSTHome.aspx.vb | Check write permissions by view | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Audit_Log | Common.vb | Record audit log entry | src/defra-wst/src/WST/Common.vb |
| sp_Audit_log_Get | Auditlog.aspx.vb | Retrieve audit log entries | src/defra-wst/src/WST/Auditlog.aspx.vb |
| sp_Audit_log_Archive | Auditlog.aspx.vb | Archive audit log | src/defra-wst/src/WST/Auditlog.aspx.vb |
| sp_Audit_log_SPList | Auditlog.aspx.vb | Get list of stored procedures for filtering | src/defra-wst/src/WST/Auditlog.aspx.vb |
| sp_Audit_log_DELETE | Common.vb | Delete audit log entries (excluded from logging) | src/defra-wst/src/WST/Common.vb |
| sp_Usage_Insert | Common.vb | Record usage statistics (excluded from logging) | src/defra-wst/src/WST/Common.vb |
| sp_Report_Facility | WSTHome.aspx.vb | Generate facility report data | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Report_Candidate | WSTHome.aspx.vb | Generate candidate report data | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Report_Instructor | WSTHome.aspx.vb | Generate instructor report data | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Report_Certification | WSTHome.aspx.vb | Generate certification report data | src/defra-wst/src/WST/WSTHome.aspx.vb |
| sp_Report_NSA | WSTHome.aspx.vb | Generate regional office report data | src/defra-wst/src/WST/WSTHome.aspx.vb |