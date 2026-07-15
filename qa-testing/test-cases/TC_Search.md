# Test Cases — Search & Discovery Feed

**Module:** Search  
**Total:** 20 test cases

---

## Search Functionality

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-046 | Search for existing track | Critical | User logged in | 1. Tap search bar 2. Type track name | Matching tracks appear in results | PASS |
| TC-047 | Search for existing artist | High | User logged in | 1. Type artist name | Artist card shown at top of results | PASS |
| TC-048 | Search for custom track (added via admin) | High | Admin added custom track | 1. Search for custom track title | Custom track appears first in results | PASS |
| TC-049 | Search for custom artist (added via admin) | High | Admin added custom artist | 1. Search for custom artist name | Custom artist card shown | PASS |
| TC-050 | Search returns no results for gibberish | Medium | User logged in | 1. Type "xyzxyzxyz" | "Nothing found" message shown | PASS |
| TC-051 | Search with empty query clears results | Medium | User searched previously | 1. Clear search input | Results list cleared | PASS |
| TC-052 | Search debounce — no request on each keystroke | Low | User typed quickly | 1. Type query fast | Network request made only after 400ms pause | PASS |
| TC-053 | Tap cancel button clears search | Medium | Search is active | 1. Tap X button | Search cleared, feed shown | PASS |
| TC-054 | Tap on track in results plays it | Critical | Search returned results | 1. Tap track in results | Player opens and track starts | PASS |
| TC-055 | Tap on artist in results opens artist profile | High | Artist found | 1. Tap artist card | Artist profile screen opens | PASS |

---

## TikTok Feed

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-056 | Discovery feed loads on search screen | High | User logged in | 1. Open Search tab | Tracks shown in vertical feed | PASS |
| TC-057 | Swipe up loads next track in feed | High | Feed is loaded | 1. Swipe up | Next track shown, audio changes | PASS |
| TC-058 | Audio muted by default | Medium | Feed loaded | 1. Observe feed | Track plays silently (muted) | PASS |
| TC-059 | Tap screen toggles audio on/off | Medium | Feed is playing | 1. Tap center of screen | Audio unmuted; tap again — muted | PASS |
| TC-060 | "For You" tab shows personalized tracks | High | User has favorites | 1. Switch to "For You" tab | Tracks from favorite artists shown | PASS |
| TC-061 | Pull to refresh reloads feed | Medium | Feed loaded | 1. Tap "Refresh" button | New tracks loaded | PASS |
| TC-062 | Feed loads more tracks at end | Medium | Near end of feed | 1. Scroll to last track | More tracks auto-loaded | PASS |
| TC-063 | Tap track title opens full player | High | Feed is active | 1. Tap track title text | Full-screen player opens | PASS |
| TC-064 | Feed stops when navigating away | Medium | Feed is playing | 1. Tap another bottom nav tab | Feed audio stops | PASS |
| TC-065 | Statistics button on feed card shows review stats | Medium | Track has ratings | 1. Tap chart icon on feed card | Stats sheet slides up with avg score | PASS |
