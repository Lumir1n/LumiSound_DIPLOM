# Checklist — Registration & Authentication

**Version:** 1.0  
**Last Updated:** July 2026

---

## Registration Form Validation

- [ ] Empty username → button disabled
- [ ] Username with only spaces → validation error
- [ ] Username with 1 character → accepted
- [ ] Username with 50+ characters → accepted or limited
- [ ] Empty email → button disabled
- [ ] Email without @ → error shown
- [ ] Email without domain → error shown
- [ ] Email with spaces → error shown
- [ ] Valid email format accepted → ✅
- [ ] Empty password → button disabled
- [ ] Password with 7 characters → "Weak" / button disabled
- [ ] Password with 8 chars, no digit → "Add digit" hint shown
- [ ] Password with 8 chars, no letter → "Add letter" hint shown
- [ ] Password meeting all requirements → "Good" indicator
- [ ] Password with special chars → "Strong" indicator
- [ ] Confirm password empty → button disabled
- [ ] Confirm password mismatch → "Passwords do not match"
- [ ] Confirm password matches → no error shown
- [ ] Submit button disabled until all valid → ✅
- [ ] Submit with valid data → account created

---

## Login Form Validation

- [ ] Empty email → button disabled
- [ ] Empty password → button disabled
- [ ] Wrong password → error message shown
- [ ] Non-existent email → error message shown
- [ ] Unconfirmed email → "Confirm your email" error
- [ ] Valid credentials → redirected to Home
- [ ] Password toggle eye icon works → ✅
- [ ] "Forgot password" link visible → ✅

---

## Session Management

- [ ] User stays logged in after app restart
- [ ] User stays logged in after device reboot
- [ ] Token refresh works after 1 hour
- [ ] Logout clears session data
- [ ] Cannot access main app after logout without login

---

## Email Confirmation

- [ ] Confirmation screen shown after registration
- [ ] Email received with confirmation link
- [ ] Clicking link confirms email
- [ ] Login possible after confirmation
- [ ] Login blocked before confirmation

---

## Password Reset

- [ ] Reset link sent to existing email
- [ ] Reset with non-existing email — no crash
- [ ] New password accepted after reset
- [ ] Old password rejected after reset
