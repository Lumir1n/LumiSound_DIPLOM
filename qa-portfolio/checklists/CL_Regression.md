# Regression Checklist — LumiSound

**Purpose:** Pre-release smoke test to verify core functionality  
**Version:** 1.0

---

## Authentication

- [ ] Register new account
- [ ] Confirm email
- [ ] Login with valid credentials
- [ ] Logout

---

## Player

- [ ] Search and play a track
- [ ] Pause and resume
- [ ] Skip to next track
- [ ] Skip to previous track
- [ ] Seek using progress bar
- [ ] Music plays in background
- [ ] Media notification shown with controls
- [ ] Sleep timer starts and stops music

---

## Search & Feed

- [ ] Search returns results for known track
- [ ] Search returns artist card
- [ ] TikTok feed loads tracks
- [ ] Swipe up shows next track
- [ ] Tap screen toggles audio
- [ ] "For You" tab loads

---

## Ratings & Reviews

- [ ] Submit rating with all 5 criteria
- [ ] Average score displayed
- [ ] Write and submit review
- [ ] Review visible in list
- [ ] Vote ↑ on review
- [ ] Reputation persists after reopen

---

## Playlists

- [ ] Create playlist
- [ ] Add track to playlist
- [ ] Play playlist
- [ ] Delete playlist

---

## Synthesis

- [ ] Create synthesis session
- [ ] Generate invite code
- [ ] Join via code
- [ ] Combined playlist created

---

## Profile

- [ ] Profile info displayed correctly
- [ ] Edit username and save
- [ ] Upload avatar
- [ ] Toggle profile visibility

---

## Settings

- [ ] Change theme (dark/light)
- [ ] Enable equalizer
- [ ] Clear cache
- [ ] About screen opens

---

## Admin Panel

- [ ] Login to admin panel
- [ ] Create artist
- [ ] Create track with audio
- [ ] Track appears in app search
- [ ] View reports

---

## Negative / Edge Cases

- [ ] No internet — app doesn't crash
- [ ] Very long username — no UI overflow
- [ ] Empty search query — no request sent
- [ ] Play track without preview URL — no crash
