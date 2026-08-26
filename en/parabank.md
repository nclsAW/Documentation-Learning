# ParaBank

## Description <a href="#description" id="description"></a>

***

ParaBank is a web-based retail banking simulation application designed specifically for software practice and testing. This application provides comprehensive online banking functionality, including opening a new account (Open New Account), checking balances and transaction history (Accounts Overview), transferring funds between accounts (Transfer Funds), paying bills (Bill Pay), applying for a loan (Apply for a Loan), as well as user profile management and database reset.

## Test Objective & Scope <a href="#test-objective-and-scope" id="test-objective-and-scope"></a>

***

* **Testing Objectives:** Validate the reliability of core banking operations, ensure the integrity of account balances and transaction history updates following financial transactions, and test the validation of inputs on transaction forms to prevent data errors.
* **In Scope:**
  * **User Onboarding & Auth:** New Account Registration (Register), Log In/Log Out, and Forgot Login Information.
  * **Account Management:** Open New Account (Checking/Savings) dan Accounts Overview (pengecekan saldo & detail transaksi).
  * **Fund Operations:** Internal Account-to-Account Transfers and Bill Pay (payments to external vendors).
  * **Credit & Loan Services:** Apply for a Loan (loan application based on balance and down payment).
  * **Customer Profile:** Update contact information and adjust address details.
* **Out of Scope:** Automated security and penetration testing, stress and load testing at the server infrastructure level, and separate backend API testing (with a focus on end-to-end manual UI testing).

## Test Environment <a href="#test-environment" id="test-environment"></a>

***

| **Parameter**        | **Detail**                                                                                |
| -------------------- | ----------------------------------------------------------------------------------------- |
| URL                  | [ParaBank \| Welcome \| Online Banking](https://parabank.parasoft.com/parabank/index.htm) |
| Browser              | Google Chrome                                                                             |
| OS                   | Windows 11                                                                                |
| Test Management Tool | Jira                                                                                      |
| Documentation Tool   | Confluence                                                                                |

## Execution Summary & Metrics <a href="#execution-summary-and-metrics" id="execution-summary-and-metrics"></a>

***

### Overall Test Case Execution Status <a href="#overall-test-case-execution-status" id="overall-test-case-execution-status"></a>

| **Status**      | **Jumlah Test Case** | **Persentase** |
| --------------- | -------------------- | -------------- |
| Passed          | 51                   | 78.46%         |
| Failed          | 14                   | 21.54%         |
| Blocked         | 0                    | 0%             |
| Total Test Case | 65                   | 100%           |

### Defect Summary by Severity <a href="#defect-summary-by-severity" id="defect-summary-by-severity"></a>

| **Severity**     | **Open** | **Resolved/Closed** | **Total Bug** |
| ---------------- | -------- | ------------------- | ------------- |
| Critical/Blocker | 3        |                     | 3             |
| High             | 8        |                     | 8             |
| Medium           |          |                     |               |
| Low/Minor        | 3        |                     | 3             |
| Total            | 14       |                     | 14            |

## Detail Break-down Task/Module <a href="#detail-break-down-task-module" id="detail-break-down-task-module"></a>

***

### Module 1: Authentication (TP-PB-0001) <a href="#module-1-authentication-tp-pb-0001" id="module-1-authentication-tp-pb-0001"></a>

* **Related Ticket:**
  * PB-0001 \[QA] User Registration
  * PB-0002 \[QA] User Login
  * PB-0003 \[QA] User Logout
* **Coverage:** Management of user login to the system, creation of new accounts, and termination of user sessions.
* **Highlight Log:**
  * The user registration process successfully created new credentials and automatically created an initial account at the same time.
  * The login and logout functions are running stably, but an issue was found regarding the lack of input sanitization for spaces in new usernames.

### Module 2: Account & Profile Management (TP-PB-0002) <a href="#module-2-account-and-profile-management-tp-pb-0002" id="module-2-account-and-profile-management-tp-pb-0002"></a>

* **Related Ticket:**
  * PB-0004 \[QA] Accounts Overview
  * PB-0005 \[QA] Find Transactions
  * PB-0006 \[QA] Update Contact Info
  * PB-0007 \[QA] Open New Account
* **Coverage:** Account information management, transaction history tracking, user profile updates, and opening additional account types (Savings/Checking).
* **Highlight Log:**
  * “Open New Account” successfully issued a new account number and accurately deducted the deposit from the main account.
  * The “Find Transactions” feature encountered a server response error when a search was performed using an empty date range.

### Module 3: Core Banking (TP-PB-0003) <a href="#module-3-core-banking-tp-pb-0003" id="module-3-core-banking-tp-pb-0003"></a>

* **Related Ticket:**
  * PB-0008 \[QA] Transfer Funds
  * PB-0009 \[QA] Bill Pay
  * PB-0010 \[QA] Request Loan
* **Coverage:** Major financial transactions involving the transfer of funds, payment of external bills, and loan applications.
* **Highlight Log:**
  * The Transfer Funds feature works smoothly and accurately updates the balances of both accounts.
  * Bill Pay has identified a critical issue where transactions with negative amounts are still being processed.
  * Request Loan consistently returns the correct decision (Approved/Denied) based on the down payment calculation.

## Key Defect Log <a href="#key-defect-log" id="key-defect-log"></a>

***

| **Jira Key** | **Bug Summary**                                                                                                                                                                                                                                                                                                                                  | **Severity** | **Status** | **Module**          |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | ---------- | ------------------- |
| KAN-20       | The system successfully terminates the session on the server upon logout, but fails to clear the browser cache because it does not set the Cache-Control header. As a result, sensitive data on the dashboard can still be viewed by other users by pressing the Back button in the browser.                                                     | Critical     | Open       | User Logout         |
| KAN-21       | Searches using fictitious data do not cause the system to crash, but the application does not provide an “Empty State” in the form of a “Data not found” message. This displays a completely empty table, which could potentially confuse users regarding the status of the search results.                                                      | Low          | Open       | Find Transactions   |
| KAN-22       | The validation on the registration form does not include a function to trim spaces and allows required fields to be left blank (except for Phone #). As a result, registration can be completed simply by entering a space character (“ ”), which risks compromising the integrity of user data in the database.                                 | High         | Open       | Register            |
| KAN-23       | The form validation on the Update Contact Info page does not trim spaces and allows required fields to be left blank without a warning (except for the Phone # field). As a result, users can update their profile data simply by entering a space character (“ ”), which risks compromising data integrity in the database.                     | High         | Open       | Update Contact Info |
| KAN-26       | The system failed to validate the availability of funds during the “Open New Account” process. The application still allowed a $100 deposit to be deducted from the source account, which had a negative balance, so the new account was successfully created while the debt on the source account continued to grow.                            | High         | Open       | Open New Account    |
| KAN-27       | The Transfer Funds feature lacks server-side validation to reject transactions that exceed the available balance limit. The system still processes large transfers ($500 from a $100 balance), causing the sender’s account to go into the red (-$400) and the recipient’s balance to increase without any confirmation of overdraft processing. | Critical     | Open       | Transfer Funds      |
| KAN-28       | The Transfer Funds feature does not enforce a minimum amount, which allows for reverse mathematical calculations involving negative numbers (-$10,000). Transactions are still processed, resulting in the sender’s balance increasing improperly and the recipient’s balance dropping into the negative.                                        | Critical     | Open       | Transfer Funds      |
| KAN-29       | The system failed to validate the availability of account options in the Transfer Funds module, thereby allowing users to select the same account number for both the sender and the recipient. Although this did not change the actual balance, the transaction was still marked as successful and generated redundant log entries.             | High         | Open       | Transfer Funds      |
| KAN-30       | The server-side validation system in the Bill Pay module does not check for sufficient funds before processing a transaction. The application still processed a $500 bill payment from an account with a balance of only $100, resulting in an unauthorized withdrawal that left the account with a negative balance of -$400.                   | High         | Open       | Bill Pay            |
| KAN-31       | The Loan Request system does not handle validation of required fields when the Down Payment field is left blank. Instead of displaying a user-friendly error message, this validation failure triggers an unhandled exception (HTTP 500) on the backend with the generic message “An internal error has occurred and has been logged.”           | High         | Open       | Request Loan        |
| KAN-32       | The “Request Loan” feature fails to validate the data type of numeric input on the application form. When a user enters non-numeric characters, the system does not catch the invalid format (on either the client or server side) and instead crashes or throws an unhandled exception (HTTP 500) on the backend.                               | High         | Open       | Request Loan        |
