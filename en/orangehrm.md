# OrangeHRM

## Description

***

OrangeHRM is a web-based Human Resources Management System (HRMS) designed to manage the entire employee lifecycle within an organization. This application provides comprehensive HR functionality, covering organizational structure and access rights management (Admin Module), personnel database management (PIM), leave configuration and requests (Leave & Attendance), performance evaluation tracking (Performance), and end-to-end recruitment workflows for job postings and candidate tracking (End-to-End Recruitment).

## Test Objective & Scope

***

* **Test Objective:** Automated security and penetration testing, stress and load testing at the server infrastructure level, third-party payroll integration testing, and separate backend API testing (with a focus on end-to-end manual UI testing)
* **In Scope:**
  * **Admin & Org Setup:** Configuration of hierarchical structures, job titles, and Role-Based Access Control (RBAC).
  * **Personnel Information (PIM):** Adding new employee data (Manual & CSV Import), custom reporting, and custom fields.
  * **Leave Management:** Configuration of leave quotas, approval workflow hierarchies, and timesheet tracking.
  * **Performance:** Developing KPIs, the performance review cycle, and tracking employee metrics.
  * **Recruitment:** Posting job openings, parsing candidate resumes, and managing interview statuses.
* **Out of Scope:** Automated Security/Penetration Testing, Stress/Load Testing di level infrastruktur server, pengujian integrasi _Payroll_ pihak ketiga, dan pengujian API _backend_ secara terpisah (fokus pada End-to-End Manual UI Testing).

## Test Environment

***

| **Parameter**        | **Detail**                                                                               |
| -------------------- | ---------------------------------------------------------------------------------------- |
| URL                  | [https://opensource-demo.orangehrmlive.com/](https://opensource-demo.orangehrmlive.com/) |
| Browser              | Google Chrome                                                                            |
| OS                   | Windows 11                                                                               |
| Test Management Tool | Jira                                                                                     |
| Documentation Tool   | Confluence                                                                               |

## Execution Summary & Metrics

***

### Overall Test Case Execution Status

| **Status**      | **Jumlah Test Case** | **Persentase** |
| --------------- | -------------------- | -------------- |
| Passed          | 95                   | 91.35%         |
| Failed          | 9                    | 8.65%          |
| Blocked         | 0                    | 0              |
| Total Test Case | 104                  | 100%           |

### Defect Summary by Severity

| **Severity**     | **Open** | **Resolved/Closed** | **Total Bug** |
| ---------------- | -------- | ------------------- | ------------- |
| Critical/Blocker | 0        | 0                   | 0             |
| High             | 8        | 0                   | 8             |
| Medium           | 0        | 0                   | 0             |
| Low/Minor        | 1        | 0                   | 1             |
| Total            | 9        | 0                   | 9             |

## Detail Break-down Task/Module

***

### Module 1: Admin Module & Organization Setup (TP-OHR-0001)

* **Related Ticket:**
  * OHR-0001 \[QA] Organization Structure
  * OHR-0002 \[QA] Job & Titles
  * OHR-0003 \[QA] User & Role Management
* **Coverage:** The company's hierarchical management structure, job title assignments, and user access rights based on role (Admin vs. ESS).
* **Highlight Log:**
  * The Organization Structure module successfully stores the company’s branch hierarchy with precision.
  * User & Role Management is functioning properly, but an access rights escalation issue (Medium) was identified in which ESS users can view the Admin configuration menu if they have a direct URL link.

### Module 2: Personnel Information Management (TP-OHR-0002)

* **Related Ticket:**
  * OHR-0004 \[QA] Add & Import Employee
  * OHR-0005 \[QA] Custom Fields & Attachments
  * OHR-0006 \[QA] Search & Custom Reporting
* **Coverage:** Manual employee data registration, bulk import via CSV, uploading attached documents, and generating operational reports.
* **Highlight Log:**
  * The “Add Employee” feature works smoothly when used manually and automatically creates a linked login profile.
  * The “Import Employee” feature encounters a critical issue when the date of birth format in the CSV file uses DD/MM/YYYY instead of the system's standard YYYY-MM-DD format.

### Module 3: Leave & Attendance Management (TP-OHR-0003)

* **Related Ticket:**
  * OHR-0007 \[QA] Leave Configuration
  * OHR-0008 \[QA] Leave Request Workflow
  * OHR-0009 \[QA] Timesheet & Attendance
* **Coverage:** Determining annual leave quotas, the process for requesting and approving leave by supervisors, and recording daily punch-in/punch-out times.
* **Highlight Log:**
  * The leave approval workflow successfully sent a real-time email notification to the relevant supervisor.
  * The system failed to validate the leave balance, allowing employees to request days off that exceeded their remaining quota without an error message.

### Module 4: Performance & Evaluation (TP-OHR-0004)

* **Related Ticket:**
  * OHR-0010 \[QA] KPIs & Key Performance Indicators
  * OHR-0011 \[QA] Performance Reviews & Employee Trackers
* **Coverage:** Development of division-specific KPI metrics and tracking of monthly/annual performance evaluations for employees.
* **Highlight Log:**
  * The performance review process (360-degree feedback) can be completed and saved accurately.
  * Employee Trackers sometimes experience delays in status synchronization (UI freeze) when saving feedback logs that contain long text.

### Module 5: End-to-End Recruitment Pipeline (TP-OHR-0005)

* **Related Ticket:**
  * OHR-0012 \[QA] Vacancies & Job Posting
  * OHR-0013 \[QA] Candidates Application
  * OHR-0014 \[QA] Shortlisting & Interview
* **Coverage:** Posting job listings, tracking the application process (resumes, shortlisting), and scheduling interviews.
* **Highlight Log:**
  * Vacancy postings link directly to the external Careers page without any issues.
  * The Shortlisting & Interview module fails to upload PDF documents larger than 5MB without displaying a validation message regarding the file size limit.

## Key Defect Log

***

| **Jira Key** | **Bug Summary**                                                                                                                                                                                                                                                                              | **Severity** | **Status** | **Module**                |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ---------- | ------------------------- |
| KAN-56       | The system successfully terminates the session on the server upon logout, but fails to clear the browser cache because it does not set the Cache-Control header. As a result, sensitive data on the dashboard can still be viewed by other users by pressing the Back button in the browser. | High         | Open       | Admin Module              |
| KAN-57       |  The system failed to stop the deletion process of the parent node even though a warning message had been displayed, resulting in the child node being accidentally deleted as well.                                                                                                         | High         | Open       | Admin Module              |
| KAN-58       |  OrangeHRM allows the deletion of job titles that are still associated with active employees without any integrity constraints, which could potentially result in orphaned records.                                                                                                          | High         | Open       | Job Titles                |
| KAN-59       |  The User Management module does not validate whether an account already exists, which allows duplicate accounts to be created for the same employee.                                                                                                                                        | High         | Open       | User Management           |
| KAN-60       |  The Custom Report Search fails to filter data if the search is performed using free text (by pressing Enter or clicking “Search”) without selecting an option from the dropdown suggestions.                                                                                                | Low          | Open       | Search & Custom Reporting |
| KAN-61       |  The system approves the registration of a new candidate using an email address that is already registered for the same vacancy without triggering a duplicate validation check.                                                                                                             | High         | Open       | Candidates Application    |
| KAN-62       |  The interview scheduling form does not include date validation, so the system still allows users to save interview schedules with past dates.                                                                                                                                               | High         | Open       | Shortlisting & Interview  |
