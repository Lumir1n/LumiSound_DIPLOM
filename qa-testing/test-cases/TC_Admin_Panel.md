# Test Cases — Admin Panel

**Module:** Admin Panel (Web)  
**Total:** 15 test cases

---

## Authentication

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-121 | Login with correct admin password | Critical | Admin panel open in browser | 1. Enter correct password 2. Tap Login | Dashboard shown | PASS |
| TC-122 | Login with wrong password | High | Admin panel open | 1. Enter wrong password 2. Tap Login | Error: "Wrong password" | PASS |
| TC-123 | Password visibility toggle | Low | Login screen | 1. Tap eye icon | Password becomes visible | PASS |

---

## Users Management

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-124 | Users list loads correctly | High | Admin logged in | 1. Open Users tab | All registered users shown | PASS |
| TC-125 | Edit user details | Medium | Users list loaded | 1. Tap edit on user 2. Change username 3. Save | User updated | PASS |
| TC-126 | Delete user | High | Users list loaded | 1. Tap delete on user 2. Confirm | User removed from list | PASS |

---

## Artists & Tracks

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-127 | Create artist with valid data | High | Artists tab open | 1. Tap "New Artist" 2. Fill name, genre 3. Upload avatar 4. Save | Artist created and visible | PASS |
| TC-128 | Upload audio file with Cyrillic filename | High | New track form | 1. Select audio file with Cyrillic name 2. Save | File uploads without "Invalid key" error | PASS |
| TC-129 | Created track appears in app search | Critical | Track created with audio | 1. Open app 2. Search track title | Custom track found in results | PASS |
| TC-130 | Track without audio shows warning | Medium | New track form | 1. Fill name only (no audio) 2. Tap Save | Error: "Audio file is required" | PASS |

---

## Reports & Bans

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-131 | Reports list shows submitted reports | High | User submitted a report | 1. Open Reports tab | Report visible with reason and user info | PASS |
| TC-132 | Ban user from reports page | High | Report visible | 1. Tap ban on reported user | User banned, shown in Bans tab | PASS |
| TC-133 | Banned user sees ban notice in app | Critical | User is banned | 1. Banned user opens Settings | Ban banner shown with reason and appeal button | PASS |
| TC-134 | Appeal submission by banned user | High | User is banned | 1. Tap "Submit Appeal" 2. Write message 3. Send | Appeal shown in admin panel Appeals tab | PASS |
| TC-135 | Dashboard statistics are accurate | Medium | Admin logged in | 1. Open Dashboard | Counts match actual DB records | PASS |
