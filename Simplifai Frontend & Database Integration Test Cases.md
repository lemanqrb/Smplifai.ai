# 🧪 Simplifai Frontend Testing Report

---

# 1️⃣ Sign Up with Valid Data

## 📌 Description

Verify that a user can successfully register with valid information.

## 📝 Steps

1. Open the Simplifai frontend registration page.
2. Enter a valid email: **leman.qrb@gmail.com**
3. Enter a valid first name: **Ləman**
4. Enter a valid password: **LDA0700fr@**
5. Re-enter the password.
6. Accept the **SMPLIFAI Terms of Use and Privacy Policy**.
7. Click the **Create an account** button.

## ✅ Expected Result

The user should be successfully registered using valid information.

## ❌ Actual Result

After email verification, the user was redirected to the home page.

## 🗄️ Database Verification

```sql
SELECT * FROM profiles
WHERE first_name = 'Ləman';
```

**Result**

```text
Test Date: 2026-04-14

id: a3c38e71-9784-4b8c-81af-9692a2aa8373
```

**Status:** ✅ PASS

---

# 2️⃣ Sign Up with an Invalid Email Address

## 📌 Description

Verify the registration process using an invalid email format.

## 📝 Steps

1. Open the Simplifai registration page.
2. Enter an invalid email: **leman123.qrbgmail.com**
3. Enter a valid first name: **Leman**
4. Enter a valid password: **LDA0700fr@**
5. Confirm the password.
6. Accept the Terms of Use and Privacy Policy.
7. Click **Create an account**.

## ✅ Expected Result

The system should detect the invalid email format and prevent registration.

## ❌ Actual Result

The account was not created, and an email validation error message was displayed.

## 🗄️ Database Verification

```sql
SELECT * FROM profiles
WHERE first_name = 'Leman';
```

**Result**

```text
No records were found because the account was not created due to the invalid email format.

Test Date: 2026-05-09
```

**Status:** ✅ PASS

---

# 3️⃣ Update Profile Information

## 📌 Description

Verify that profile information can be updated successfully.

## 📝 Steps

1. Navigate to the **Profile** page.
2. Change the first name.
3. Keep the last name unchanged.
4. Keep the phone number unchanged.
5. Click **Send Code**.
6. Leave the email unchanged.
7. Click **Save Changes**.

## ✅ Expected Result

The profile should be updated successfully.

## ❌ Actual Result

The message **"Profile updated successfully!"** was displayed.

## 🗄️ Database Verification

```sql
SELECT * FROM profiles
WHERE first_name = 'Lale';
```

**Result**

```text
The user exists with ID:

a3c38e71-9784-4b8c-81af-9692a2aa8373
```

**Status:** ✅ PASS

---

# 4️⃣ Log Out from the System

## 📌 Description

Verify that the user can successfully log out.

## 📝 Steps

1. Log in to Simplifai.
2. Open the **Profile** page.
3. Click the **Log Out** button.

## ✅ Expected Result

The user should be logged out and redirected to the login page.

## ❌ Actual Result

The user session was terminated successfully, and the login page was displayed.

## 🗄️ Database Verification

```sql
SELECT * FROM profiles
WHERE first_name = 'Leman';
```

**Result**

```text
The user is no longer present in the active session because logout was completed successfully.

Test Date: 2026-05-09
```

**Status:** ✅ PASS

---

# 5️⃣ Sign In with Google

## 📌 Description

Verify successful login using a valid Google account.

## 📝 Steps

1. Open the login page.
2. Click **Sign in with Google**.
3. Select the Google account **lilithate601@gmail.com**.
4. Enter the phone number **0559448073**.
5. Click **Confirm**.

## ✅ Expected Result

The user account should be created (if necessary) and successfully signed in.

## ❌ Actual Result

The account was created successfully, and the user logged in.

## 🗄️ Database Verification

```sql
SELECT * FROM profiles
WHERE first_name = 'Lilith';
```

**Result**

```text
User exists with ID:

fb5d2633-580a-4683-9ed9-d42d23a84b43
```

**Status:** ✅ PASS

---

# 6️⃣ Log In with an Invalid Password

## 📌 Description

Verify system behavior when an incorrect password is entered.

## 📝 Steps

1. Open the login page.
2. Enter the email **moonloor22@gmail.com**.
3. Enter the invalid password **1234679sd**.
4. Click **Log In**.

## ✅ Expected Result

The system should display the **"Invalid login credentials"** error message and deny access.

## ❌ Actual Result

The expected error message was displayed, and the user could not log in.

## 🗄️ Database Verification

```sql
SELECT * FROM profiles
WHERE email = 'leman.qrb@gmail.com';
```

**Result**

```text
The user exists in the database, but authentication failed because the entered password was incorrect.

Test Date: 2026-05-09
```

**Status:** ✅ PASS

---

# 7️⃣ Update Profile with Invalid Input

## 📌 Description

Verify validation when special characters are entered into the first name field.

## 📝 Steps

1. Open the **Profile** page.
2. Enter **#$%&*** as the first name.
3. Keep the phone number unchanged.
4. Click **Send Code**.
5. Leave the email unchanged.
6. Click **Save Changes**.

## ✅ Expected Result

The system should reject the input and display a validation error message.

## ❌ Actual Result

```diff
- "Profile updated successfully!" was displayed.
```

## 🗄️ Database Verification

```sql
SELECT * FROM profiles
WHERE first_name = '#$%&*';
```

**Result**

```text
The user exists with ID:

a3c38e71-9784-4b8c-81af-9692a2aa8373
```

**Status:** ❌ FAIL

---

# 8️⃣ Create a New Application with Valid Data

## 📌 Description

Verify that a new application can be created using valid information.

## 📝 Steps

1. Open the **Dashboard**.
2. Click **New Application**.
3. Enter a valid email and phone number.
4. Click **Choose**.
5. Upload an image.
6. Click **Submit Passport to Review**.
7. Fill in the first name and last name.
8. Click **Approve**.

## ✅ Expected Result

A new application should be created successfully.

## ❌ Actual Result

The application was successfully created and appeared in the Dashboard/History section.

## 🗄️ Database Verification

```sql
SELECT * FROM applications
WHERE created_at = '2026-05-27 15:56:12.376057+00';
```

**Result**

```text
Application exists with ID:

6051ddcc-1afd-41a4-9db8-f587e3a4213e
```

**Status:** ✅ PASS

---

# 9️⃣ Create a New Application with Invalid Phone Number

## 📌 Description

Verify validation when an invalid phone number format is entered.

## 📝 Steps

1. Open the **Dashboard**.
2. Click **New Application**.
3. Enter a valid email.
4. Enter special characters instead of a phone number.
5. Click **Choose**.
6. Upload an image.
7. Click **Submit Documents**.

## ✅ Expected Result

The system should reject the request and display a validation error.

## ❌ Actual Result

```diff
- The "Enrollment Agreement" application was created successfully.
```

## 🗄️ Database Verification

```sql
SELECT * FROM applications
WHERE phone = '+44@#$%^&*()';
```

**Result**

```text
Application exists with ID:

8c172506-d34f-4d5a-b2d3-eb9f613882db
```

**Status:** ❌ FAIL

---

# 🔟 Verify PDF Download from the History Page

## 📌 Description

Verify that PDF files can be downloaded successfully from the **History** page.

## 📝 Steps

1. Open the **History** page.
2. In **Application History**, click the PDF download icon next to any application.

## ✅ Expected Result

The PDF file should download successfully, and a download confirmation should appear.

## ❌ Actual Result

A confirmation notification indicating that the PDF was downloaded successfully was displayed.

**Status:** ✅ PASS
