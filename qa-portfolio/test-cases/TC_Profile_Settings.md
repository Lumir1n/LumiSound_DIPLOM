# Test Cases — Profile & Settings

**Module:** Profile & Settings  
**Total:** 15 test cases

---

## Profile

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-106 | Profile screen shows correct user info | High | User logged in | 1. Open Profile tab | Username, avatar, bio displayed correctly | PASS |
| TC-107 | Edit username | High | Profile screen open | 1. Tap pencil icon 2. Change username 3. Save | New username saved and displayed | PASS |
| TC-108 | Edit bio | Medium | Profile screen open | 1. Tap edit 2. Change bio 3. Save | Bio updated | PASS |
| TC-109 | Upload avatar from gallery | High | Profile edit screen | 1. Tap avatar 2. Select image 3. Crop 4. Save | New avatar shown on profile | PASS |
| TC-110 | Profile shows favorite tracks | Medium | Tracks listened | 1. Open Profile | Favorite tracks sorted by play count shown | PASS |
| TC-111 | Profile shows favorite artists | Medium | Artists listened | 1. Open Profile | Favorite artists sorted by play count | PASS |
| TC-112 | Toggle profile public/private | High | Profile screen | 1. Settings → Privacy → Toggle | Profile visibility updated | PASS |
| TC-113 | Public profile visible by other users | High | Profile is public | 1. Another user navigates to profile | Profile visible | PASS |

---

## Settings

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-114 | Switch to light theme | Medium | Settings open | 1. Appearance → Light | App switches to light theme | PASS |
| TC-115 | Switch to dark theme | Medium | Settings open | 1. Appearance → Dark | App switches to dark theme | PASS |
| TC-116 | Change app icon | Low | Settings open | 1. App Icon → Select "Blue" | App icon changes on home screen | PASS |
| TC-117 | Clear cache | Medium | Settings open | 1. Data → Clear Cache 2. Confirm | Toast shown: cache cleared | PASS |
| TC-118 | About screen opens with policies | Low | Settings open | 1. Tap "About" | Screen shows copyright, privacy policy, terms | PASS |
| TC-119 | Back gesture from About returns to Settings | Medium | About screen open | 1. Android back gesture | Returns to Settings, not Profile | PASS |
| TC-120 | Logout stops music and clears session | High | Track playing | 1. Settings → Logout → Confirm | Music stops, user redirected to Welcome screen | PASS |
