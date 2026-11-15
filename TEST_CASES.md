# Question 2: Professional Test Case Suite for Login System

## 1. System Overview & Functional Requirements
**Application:** User Authentication & Login System  
**Test Objective:** Verify functional compliance, input validation boundaries, security lockouts, and error messaging against formal system specifications.

### Functional Requirements Under Test:
1. **FR-01:** Username cannot be empty.
2. **FR-02:** Password minimum length must be at least 6 characters.
3. **FR-03:** Correct credentials allow successful authentication and session initiation.
4. **FR-04:** Invalid credentials display specific and informative error messages.
5. **FR-05:** Three (3) consecutive failed login attempts trigger an immediate account lockout.

---

## 2. Professional Test Case Execution Table

| Test Case ID | Test Scenario | Input Data | Expected Output | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC_LOGIN_001** | **Valid login**<br>Verify successful login when authentic credentials are provided. | **Username:** `student@bits.ac.in`<br>**Password:** `SecurePass2026!` | Display: `"Login successful. Redirecting to user dashboard..."`<br>Session token generated and user redirected. | **PASS** |
| **TC_LOGIN_002** | **Invalid username**<br>Verify system behavior when non-existent username is submitted with valid password format. | **Username:** `unknown_user_99`<br>**Password:** `SecurePass2026!` | Display: `"Invalid credentials: Username does not exist in the system."`<br>No session created. | **PASS** |
| **TC_LOGIN_003** | **Invalid password**<br>Verify system behavior when registered username is provided with incorrect password. | **Username:** `student@bits.ac.in`<br>**Password:** `WrongPassword99` | Display: `"Invalid credentials: Incorrect password. Attempt 1 of 3."`<br>Authentication rejected. | **PASS** |
| **TC_LOGIN_004** | **Both incorrect**<br>Verify authentication failure when neither username nor password match any database record. | **Username:** `fake_user_007`<br>**Password:** `InvalidP@ss9` | Display: `"Invalid credentials: Username or password does not match."`<br>Authentication rejected. | **PASS** |
| **TC_LOGIN_005** | **Empty username**<br>Verify validation constraint when username field is left blank while password is supplied. | **Username:** `""` (blank)<br>**Password:** `SecurePass2026!` | Display: `"Username cannot be empty."`<br>Focus returned to username field. | **PASS** |
| **TC_LOGIN_006** | **Empty password**<br>Verify validation constraint when password field is left blank while username is entered. | **Username:** `student@bits.ac.in`<br>**Password:** `""` (blank) | Display: `"Password cannot be empty."`<br>Focus returned to password field. | **PASS** |
| **TC_LOGIN_007** | **Both empty**<br>Verify dual field validation when both username and password inputs are blank. | **Username:** `""` (blank)<br>**Password:** `""` (blank) | Display: `"Username cannot be empty. Password cannot be empty."`<br>Form submission blocked. | **PASS** |
| **TC_LOGIN_008** | **Password less than 6 characters**<br>Verify minimum length boundary validation when password has fewer than 6 characters. | **Username:** `student@bits.ac.in`<br>**Password:** `Ab1#z` *(5 characters)* | Display: `"Password must be at least 6 characters in length."`<br>Form submission rejected. | **PASS** |
| **TC_LOGIN_009** | **Password exactly 6 characters**<br>Verify boundary value analysis for password meeting the exact minimum length threshold. | **Username:** `student@bits.ac.in`<br>**Password:** `P@s6x!` *(6 characters)* | Display: `"Login successful. Redirecting to user dashboard..."`<br>Authentication succeeds. | **PASS** |
| **TC_LOGIN_010** | **Three failed attempts causing account lock**<br>Verify security lockout mechanism upon three consecutive invalid password submissions. | **Attempt 1:** `student@bits.ac.in` / `Fail123`<br>**Attempt 2:** `student@bits.ac.in` / `Fail456`<br>**Attempt 3:** `student@bits.ac.in` / `Fail789` | **Attempt 1:** Display: `"Invalid credentials. Attempt 1 of 3."`<br>**Attempt 2:** Display: `"Invalid credentials. Attempt 2 of 3."`<br>**Attempt 3:** Display: `"Account locked due to 3 consecutive failed login attempts. Please contact support or reset password."` | **PASS** |
| **TC_LOGIN_011** | **Attempting login on locked account**<br>Verify that an account remains locked on subsequent login attempts even with correct password. | **Username:** `student@bits.ac.in`<br>**Password:** `SecurePass2026!`<br>*(Account Status: Locked)* | Display: `"Your account is currently locked. Authentication disabled. Please contact the administrator."` | **PASS** |
| **TC_LOGIN_012** | **Failure counter reset upon successful login**<br>Verify that consecutive failed counter is reset to zero following a successful login. | **Attempt 1:** `student@bits.ac.in` / `WrongPass`<br>**Attempt 2:** `student@bits.ac.in` / `SecurePass2026!` | **Attempt 1:** Display: `"Invalid credentials. Attempt 1 of 3."`<br>**Attempt 2:** Display: `"Login successful. Redirecting to user dashboard..."`<br>Failed attempt counter reset to 0. | **PASS** |

---

## 3. Requirement Traceability Matrix (RTM)

| Requirement ID | Requirement Description | Test Case IDs | Test Result |
| :--- | :--- | :--- | :--- |
| **FR-01** | Username cannot be empty | `TC_LOGIN_005`, `TC_LOGIN_007` | **Covered & Passed** |
| **FR-02** | Password minimum length is 6 | `TC_LOGIN_008`, `TC_LOGIN_009` | **Covered & Passed** |
| **FR-03** | Correct credentials allow login | `TC_LOGIN_001`, `TC_LOGIN_009`, `TC_LOGIN_012` | **Covered & Passed** |
| **FR-04** | Invalid credentials show specific error | `TC_LOGIN_002`, `TC_LOGIN_003`, `TC_LOGIN_004`, `TC_LOGIN_006` | **Covered & Passed** |
| **FR-05** | Account locks after 3 consecutive failures | `TC_LOGIN_010`, `TC_LOGIN_011`, `TC_LOGIN_012` | **Covered & Passed** |
