# 🐞 Bug Report

| Field | Details |
|-------|---------|
| **Bug ID** | BUG_002 |
| **Title** | New Application accepts special characters in the Phone Number field |
| **Description** | The system allows users to enter special characters in the **Phone Number** field when creating a new application. The invalid input passes validation, and the application is created successfully. |
| **Steps to Reproduce** | 1. Navigate to the **Dashboard** page in the Simplifai frontend.<br>2. Click the **New Application** button.<br>3. Enter a valid email address and other required information.<br>4. Enter special characters instead of digits in the **Phone Number** field.<br>5. Click the **Choose** button.<br>6. Upload an image.<br>7. Click the **Submit Documents** button. |
| **Expected Result** | The system should reject the invalid phone number and display a validation error message. The application should not be created. |
| **Actual Result** | The **"Enrollment Agreement"** application was created successfully despite the invalid phone number. |
| **Priority** | Medium |
| **Severity** | Major |
| **Status** | Open / Confirmed |
| **Date Reported** | 27.05.2026 |
| **Reported By** | Ləman Qurbanova |
| **Attachments** | <img width="974" height="445" alt="Bug Screenshot" src="https://github.com/user-attachments/assets/a84b7989-b0c0-4ed0-a3ec-a75132582d52" /> |
