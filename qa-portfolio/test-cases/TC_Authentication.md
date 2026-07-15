# Test Cases — Authentication

**Module:** Authentication  
**Total:** 20 test cases

---

## Registration

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-001 | Successful registration with valid data | High | App is open, user is not logged in | 1. Tap "Create Account" 2. Enter valid username 3. Enter valid email 4. Enter strong password (8+ chars, letter+digit) 5. Confirm password 6. Tap "Create Account" | Account created, email confirmation screen shown | PASS |
| TC-002 | Registration with already existing email | High | TC-001 passed, email is in DB | 1. Repeat TC-001 with same email | Error message shown: "Email already in use" | PASS |
| TC-003 | Registration with empty username | Medium | App is open | 1. Leave username empty 2. Fill other fields 3. Tap "Create Account" | Button disabled or error: "Username required" | PASS |
| TC-004 | Registration with invalid email format | Medium | App is open | 1. Enter "notanemail" in email field | Error: "Enter valid email" shown below field | PASS |
| TC-005 | Registration with password less than 8 characters | Medium | App is open | 1. Enter password "abc123" | Strength indicator shows "Weak", button disabled | PASS |
| TC-006 | Registration with mismatched passwords | Medium | App is open | 1. Enter password "Test1234" 2. Enter confirm "Test5678" | Error: "Passwords do not match" | PASS |
| TC-007 | Password strength indicator — weak | Low | App is open | 1. Enter password "123" | Strength bar shows 1/3, label "Weak" | PASS |
| TC-008 | Password strength indicator — strong | Low | App is open | 1. Enter password "Test1234!" | Strength bar shows 3/3, label "Strong" | PASS |

---

## Login

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-009 | Successful login with valid credentials | Critical | User is registered and email confirmed | 1. Enter registered email 2. Enter correct password 3. Tap "Login" | User redirected to Home screen | PASS |
| TC-010 | Login with wrong password | High | User is registered | 1. Enter registered email 2. Enter wrong password 3. Tap "Login" | Error: "Invalid email or password" | PASS |
| TC-011 | Login with non-existent email | High | App is open | 1. Enter "notexist@test.com" 2. Enter any password 3. Tap "Login" | Error: "Invalid email or password" | PASS |
| TC-012 | Login with empty fields | Medium | App is open | 1. Leave both fields empty 2. Tap "Login" | Button disabled or validation errors shown | PASS |
| TC-013 | Login with unconfirmed email | High | User registered but email not confirmed | 1. Enter credentials of unconfirmed account 2. Tap "Login" | Error: "Please confirm your email" | PASS |
| TC-014 | Password visibility toggle | Low | Login screen is open | 1. Enter password 2. Tap eye icon | Password becomes visible; tap again — hidden | PASS |

---

## Email Confirmation

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-015 | Email confirmation screen shown after registration | High | Registration completed | 1. Complete registration | Screen shown with instruction to confirm email | PASS |
| TC-016 | App accessible after email confirmation | Critical | Email confirmed via link | 1. Click confirmation link in email 2. Open app 3. Login | User can login successfully | PASS |

---

## Password Reset

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-017 | Password reset email sent for existing account | High | User is registered | 1. Tap "Forgot Password" on Login screen 2. Enter registered email 3. Tap "Send" | Toast: "Email sent to [email]" | PASS |
| TC-018 | Password reset with non-existing email | Medium | Login screen open | 1. Tap "Forgot Password" 2. Enter non-existing email | Toast or error shown; no crash | PASS |
| TC-019 | Navigation: Login → Register → Login | Low | App open | 1. Tap "Create Account" 2. Tap "Already have account?" | Returns to Login screen | PASS |
| TC-020 | Session persists after app restart | High | User is logged in | 1. Close app completely 2. Reopen app | User remains logged in, Home screen shown | PASS |
