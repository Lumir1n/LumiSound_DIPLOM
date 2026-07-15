# Test Cases — Playlists & Synthesis

**Module:** Playlists  
**Total:** 20 test cases

---

## Playlists

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-086 | Create new playlist | High | User logged in | 1. Home → Playlists 2. Tap "+" 3. Enter name 4. Confirm | Playlist created and shown in list | PASS |
| TC-087 | Add track to playlist | High | Playlist exists, track playing | 1. In player tap "+" 2. Select playlist | Track added, count incremented | PASS |
| TC-088 | Remove track from playlist | Medium | Track in playlist | 1. Open playlist 2. Long press track 3. Remove | Track removed, count decremented | PASS |
| TC-089 | Delete playlist | Medium | Playlist exists | 1. Long press playlist 2. Delete | Playlist removed from list | PASS |
| TC-090 | Rename playlist | Medium | Playlist exists | 1. Open playlist 2. Tap edit 3. Change name | New name saved and displayed | PASS |
| TC-091 | Toggle playlist visibility public/private | Medium | Playlist exists | 1. Open playlist 2. Toggle visibility | Icon changes, visibility updated | PASS |
| TC-092 | Public playlist visible in search | Medium | Public playlist created | 1. Search playlist name | Playlist appears in search results | PASS |
| TC-093 | Private playlist not visible in search | Medium | Private playlist created | 1. Search playlist name from another account | Playlist not shown | PASS |
| TC-094 | Upload playlist cover image | Low | Playlist exists | 1. Open playlist 2. Tap cover 3. Select image | New cover image shown | PASS |
| TC-095 | Play all tracks in playlist | High | Playlist has 3+ tracks | 1. Open playlist 2. Tap Play All | All tracks queue up and play sequentially | PASS |

---

## Synthesis Sessions

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-096 | Create synthesis session | High | User logged in | 1. Home → Synthesis 2. Tap "Create" | Session created, invite code shown | PASS |
| TC-097 | Invite code is 8 hex characters | Medium | Session created | 1. Observe invite code | Code matches pattern (e.g. "44f9817e") | PASS |
| TC-098 | Join synthesis session via code | High | Session created by user A | 1. User B: enter invite code 2. Tap "Join" | User B joined, participants list updated | PASS |
| TC-099 | Joint playlist created after both join | High | Both users joined session | 1. Session starts | Combined playlist from both users' favorites shown | PASS |
| TC-100 | Cannot join with invalid invite code | Medium | Join screen open | 1. Enter "00000000" (invalid) 2. Tap Join | Error: "Session not found" | PASS |
| TC-101 | Leave synthesis session | Medium | User is in a session | 1. Tap "Leave" | User removed from session | PASS |
| TC-102 | Existing synthesis shown on home screen | Medium | Synthesis created | 1. Open Home | Synthesis card visible in playlists section | PASS |
| TC-103 | Play synthesis playlist | High | Synthesis playlist exists | 1. Tap synthesis playlist 2. Play | Tracks play in order | PASS |
| TC-104 | Synthesis session reuses existing if same friends | Medium | Previous synthesis with same user exists | 1. Create synthesis with same friend | Existing synthesis shown instead of new | PASS |
| TC-105 | Synthesis tracks visible to both participants | High | Synthesis created | 1. Both users open synthesis playlist | Same tracks visible for both | PASS |
