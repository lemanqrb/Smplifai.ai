# 🐞 Bug Report

| Field | Details |
|-------|---------|
| **Bug ID** | BUG_003 |
| **Title** | Profile update accepts special characters in the First Name field |
| **Description** | The system allows users to enter special characters in the **First Name** field and successfully updates the profile without displaying any validation error. |
| **Steps to Reproduce** | 1. Navigate to the **Profile** page in the Simplifai frontend.<br>2. Enter **"#$%&*"** in the **First Name** field.<br>3. Leave the phone number unchanged.<br>4. Click the **Send Code** button.<br>5. Leave the email address unchanged.<br>6. Click the **Save Changes** button. |
| **Expected Result** | The system should reject the invalid input and display a validation error message. The profile should not be updated. |
| **Actual Result** | The message **"Profile updated successfully!"** was displayed, and the profile was updated with the invalid value. |
| **Priority** | Medium |
| **Severity** | Major |
| **Status** | Open / Confirmed |
| **Date Reported** | 27.05.2026 |
| **Reported By** | Ləman Qurbanova |
| **Attachments** | <img width="974" height="466" alt="Bug Screenshot" src="https://github.com/user-attachments/assets/c3da3e16-81c1-4b96-b514-244bad49b709" /> |
