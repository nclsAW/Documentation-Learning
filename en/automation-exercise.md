# Automation Exercise

## Description <a href="#description" id="description"></a>

***

This document summarizes the scope of end-to-end (E2E) functional testing of the web interface (UI) and Application Programming Interface (API) integration on the Automation Exercise platform. The testing covers the complete e-commerce cycle, ranging from user account management, product catalog browsing, shopping cart management, transaction and checkout workflows, customer support, general navigation, to the validation of the REST API backend layer.

## Test Objective & Scope <a href="#test-objective-and-scope" id="test-objective-and-scope"></a>

***

### Test Objective: <a href="#test-objective" id="test-objective"></a>

* Ensure that all key functional features (authentication, catalog, shopping cart, order/checkout, and contact form) operate in accordance with business process specifications.
* Validate data consistency between the front-end user interface and the back-end REST API.
* Identify workflow failures, form validation discrepancies, and status codes/JSON formats in API endpoints.

### In-Scope: <a href="#in-scope" id="in-scope"></a>

* **TP-0001:** Account registration, user data and address validation, login (valid/invalid), duplicate email detection, active session status, logout, and account deletion.
* **TP-0002**: Catalog navigation (/products), product details, search bar, Category/Subcategory filters, Brand filters, and product review submission.
* **TP-0003**: Catalog navigation (/products), product details, search bar, Category/Subcategory filters, Brand filters, and product review submission.
* **TP-0004**: Checkout process (3 scenario variations), shipping/billing address verification, payment card entry, order confirmation (Order Placed), and invoice download (PDF).
* **TP-0005**: Navigating the “Contact Us” page, filling out the form, uploading file attachments, handling JavaScript pop-up dialogs (Alert OK), and displaying a success confirmation message.
* **TP-0006**: Page navigation for Test Cases, newsletter subscription (footer subscription) on the Home and Cart pages, and the scroll-up button (button and manual).
* **TP-0007**: REST API endpoint validation (GET, POST, PUT, DELETE) includes HTTP status codes (200, 201, 400, 404, 405), JSON payload structure, and backend error messages.

### Out-of-Scope: <a href="#out-of-scope" id="out-of-scope"></a>

* “Forgot/Reset Password” feature and third-party OAuth authentication (Google/Facebook).
* Product sorting (by price/alphabetically) and an AI/ML-based recommendation system.
* Inline editing of product quantities directly in the cart and the use of voucher/promo codes.
* Live payment gateway integration with 3D Secure and OTP verification.
* Automatic email notifications and blasts via external SMTP, and integration with third-party helpdesk and CRM systems.
* Performance testing, load and stress testing, penetration testing, and cross-browser responsiveness testing for legacy and mobile layouts.

## Test Environment <a href="#test-environment" id="test-environment"></a>

***

| **Parameter**        | **Detail**                                             |
| -------------------- | ------------------------------------------------------ |
| URL                  | [Automation Exercise](https://automationexercise.com/) |
| Browser              | Google Chrome                                          |
| OS                   | Windows 11                                             |
| Test Management Tool | Jira                                                   |
| Documentation Tool   | Confluence                                             |

## Execution Summary & Metrics <a href="#execution-summary-and-metrics" id="execution-summary-and-metrics"></a>

***

### Overall Test Case Execution Status <a href="#overall-test-case-execution-status" id="overall-test-case-execution-status"></a>

| **Status**      | **Jumlah Test Case** | **Persentase** |
| --------------- | -------------------- | -------------- |
| Passed          | 60                   | 98%            |
| Failed          | 2                    | 2%             |
| Blocked         | 0                    | 0%             |
| Total Test Case | 62                   | 100%           |

### Defect Summary by Severity <a href="#defect-summary-by-severity" id="defect-summary-by-severity"></a>

| **Severity**     | **Open** | **Resolved/Closed** | **Total Bug** |
| ---------------- | -------- | ------------------- | ------------- |
| Critical/Blocker | 0        | 0                   | 0             |
| High             | 1        | 0                   | 1             |
| Medium           | 1        | 0                   | 1             |
| Low/Minor        | 0        | 0                   | 0             |
| Total            | 2        | 0                   | 2             |

## Detail Break-down Task/Module <a href="#detail-break-down-task-module" id="detail-break-down-task-module"></a>

***

### Module 1: Authentication & Account Management (TP-AEX-0001) <a href="#module-1-authentication-and-account-management-tp-aex-0001" id="module-1-authentication-and-account-management-tp-aex-0001"></a>

* **Related Ticket:**
  * AEX-0001 \[QA] User Registration & Account Creation
  * AEX-0002 \[QA] User Login & Session Management
* **Coverage**: User account lifecycle management includes new registrations, validation of login and logout credentials, handling duplicate email addresses, verifying active session status, and permanent account deletion.
* **Highlight Log:**
  * The registration, login, and account deletion workflows were successfully validated, with the data synchronized and stored in the database.
  * The validation error for duplicate email registration appeared as expected (“Email Address Already Exists!”).

### Module 2: Product Catalog, Search & Review (TP-AEX-0002) <a href="#module-2-product-catalog-search-and-review-tp-aex-0002" id="module-2-product-catalog-search-and-review-tp-aex-0002"></a>

***

* **Related Ticket:**
  * AEX-0003 \[QA] Product Browsing & Category Filter
* **Coverage**: Browsing the product catalog, navigating the category/subcategory hierarchy, filtering by brand, using the search bar, and submitting product reviews.
* **Highlight Log:**
  * Searching and filtering by category/brand displays relevant products without broken images.
  * The product review form successfully submits the data and displays a success notification (“Thank you for your review.”).

### Module 3: Cart Management & Recommended Items (TP-AEX-0003) <a href="#module-3-cart-management-and-recommended-items-tp-aex-0003" id="module-3-cart-management-and-recommended-items-tp-aex-0003"></a>

***

* R**elated Ticket:**
  * AEX-0004 \[QA] Cart Operations & Items Persistence
* **Coverage**: Adding products to the shopping cart, adjusting item quantities, adding items via the “Recommended Items” widget, removing items, calculating subtotals and totals, and retaining cart data after logging in.
* **Highlight Log:**
  * Price calculations and shopping cart contents persistence when switching session statuses (from guest to logged in) are functioning normally.
  * An anomaly was found with the shopping cart badge counter in the navigation bar, which does not update automatically when items are added from “Recommended Items” without reloading the page.

### Module 4: Checkout, Payment & Order Processing (TP-AEX-0004) <a href="#module-4-checkout-payment-and-order-processing-tp-aex-0004" id="module-4-checkout-payment-and-order-processing-tp-aex-0004"></a>

***

* R**elated Ticket:**
  * AEX-0005 \[QA] Checkout Flow & Order Confirmation
  * AEX-0006 \[QA] Payment Execution & Invoice Download
* **Coverage**: Validation of the end-to-end checkout flow (3 scenario flows), verification of the integrity of shipping/billing address data, payment card form input, order confirmation, and invoice file download.
* **Highlight Log:**
  * All three checkout flow scenarios leading up to order placement (Order Placed!) were processed smoothly.
  * An issue was found with the invoice download feature, where the generated PDF file was empty (0 KB).

### Module 5: Customer Support & Contact Us (TP-AEX-0005) <a href="#module-5-customer-support-and-contact-us-tp-aex-0005" id="module-5-customer-support-and-contact-us-tp-aex-0005"></a>

***

* R**elated Ticket:**
  * AEX-0007 \[QA] Contact Us Submission & File Attachment
* **Coverage**: Testing the customer support form, uploading file attachments, handling JavaScript pop-up confirmation dialogs (Alert OK), verifying success notifications, and the “Back to Main Page” button.
* **Highlight Log:**
  * The browser alert confirmation was handled automatically, and the contact form was successfully submitted (“Success! Your details have been submitted successfully.”).
  * Upload file type validation works reliably for common formats (documents/images).

### Module 6: UI, Navigation & Footer Subscription (TP-AEX-0006) <a href="#module-6-ui-navigation-and-footer-subscription-tp-aex-0006" id="module-6-ui-navigation-and-footer-subscription-tp-aex-0006"></a>

***

* R**elated Ticket:**
  * AEX-0008 \[QA] Page Navigation & Scroll Behavior
  * AEX-0009 \[QA] Footer Email Subscription
* **Coverage**: Validate the static menu navigation, verify the newsletter sign-up function in the footer on various pages, and test the automatic and manual scroll-up button functions.
* **Highlight Log:**
  * The newsletter subscription form instantly displays a success message (“You have been successfully subscribed!”).
  * The “Scroll Up” button animation moves smoothly, returning the viewport to the top of the page.

### Module 7: Backend API Testing Validation (TP-AEX-0007) <a href="#module-7-backend-api-testing-validation-tp-aex-0007" id="module-7-backend-api-testing-validation-tp-aex-0007"></a>

***

* R**elated Ticket:**
  * AEX-0010 \[QA] Products & Brands API Validation
  * AEX-0011 \[QA] Authentication & User Account API Validation
* **Coverage**: Validation of the REST API backend interface includes verifying the HTTP status codes (200, 201, 400, 404, 405), the JSON schema of the response payload, and the accuracy of the error response messages.
* **Highlight Log:**
  * All endpoints for creating, updating, logging in, and deleting accounts via the API successfully interacted directly with the database.
  * An inconsistency was found in the status code scheme for the POST /api/searchProduct endpoint, which continues to return a 200 OK status even when required parameters are not sent.

## Key Defect Log <a href="#key-defect-log" id="key-defect-log"></a>

***

| **Jira Key** | **Bug Summary**                                                                                                                                                                                                                                  | **Severity** | **Status** | **Module**     |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | ---------- | -------------- |
| KAN-83       | The absence of a minimum value validation (< 1) for the “Quantity” input risks corrupting the total price calculation and inventory logic, and may result in a negative subtotal if a value greater than or equal to 0 is processed at checkout. | S2           | Open       | Cart Module    |
| KAN-84       | The payment form accepts card numbers with fewer digits than the industry standard without validation (e.g., Luhn algorithm/standard 16-digit length), potentially allowing invalid payloads to pass through to the payment gateway.             | S1           | Open       | Payment Module |
