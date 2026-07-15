# Exploratory Testing Sessions — LumiSound

---

## Session 1 — Authentication & Onboarding

**Date:** July 2026  
**Duration:** 45 minutes  
**Focus:** Registration, login, edge cases  
**Tester:** Miroslav Gilevich

### Charter
Explore authentication flows looking for validation gaps, navigation issues, and unexpected error states.

### Notes
- Tried pasting email with trailing space — accepted, but login fails silently (space included in email)
- Password field loses focus when switching to email field on some keyboards
- Pressing "Create Account" twice quickly — only one request sent ✅
- Long username (50+ chars) accepted — no UI overflow on profile screen ✅
- Cyrillic username works correctly in all screens ✅
- "Forgot password" link is small and hard to tap on small screens

### Bugs Found
- **BUG-018** — Registration form doesn't scroll to error field when keyboard is open

---

## Session 2 — Player Stress Testing

**Date:** July 2026  
**Duration:** 60 minutes  
**Focus:** Player controls, queue, audio/visual sync  
**Tester:** Miroslav Gilevich

### Charter
Stress test the music player — rapid next/prev, seek while loading, switch tracks while paused.

### Notes
- Tapping "Next" 5 times rapidly — player handles it correctly, no crash ✅
- Seeking before track is fully loaded — sometimes shows incorrect position
- Swipe left/right very fast — occasional frame skip but no crash ✅
- Background playback stable for 30+ minutes ✅
- Incoming phone call pauses music correctly ✅
- After call ends, music does NOT auto-resume (expected on Android 12+) ✅
- Sleep timer with 1 minute: counts correctly, stops exactly on time ✅
- Waveform visualization is deterministic (same track = same waveform) ✅

### Bugs Found
- **BUG-003** — Audio/visual desync when appending to queue (already fixed)
- Seek bar position jumps slightly when progress updates during drag

---

## Session 3 — Reviews & Social Features

**Date:** July 2026  
**Duration:** 50 minutes  
**Focus:** Ratings, reviews, voting, reports  
**Tester:** Miroslav Gilevich

### Charter
Explore the review system — submit ratings, vote, report, check data integrity.

### Notes
- Rating with all sliders at 1 → overall score shows 1.0 ✅
- Rating with all sliders at 10 → overall score shows 10.0 ✅
- Voting on own review — arrows greyed out ✅
- Voting up then down — reputation goes from +1 to -1 (correct delta) ✅
- Long pressing own comment — no report dialog (correct) ✅
- Long pressing other's comment — report dialog appears ✅
- Report dialog: selecting reason and confirming — "Report submitted" shown ✅
- Very long review text (500+ chars) — no crash, truncated with "..." ✅
- Submitting review with only whitespace — trimmed, rejected ✅

### Bugs Found
- **BUG-002** — Reputation not saved (fixed via RPC function)
- **BUG-010** — Vote state lost after reopen (fixed via `getMyVotesForReviews`)

---

## Session 4 — Search & Discovery

**Date:** July 2026  
**Duration:** 40 minutes  
**Focus:** Search results, feed behavior, artist profiles  
**Tester:** Miroslav Gilevich

### Charter
Test search with various query types, feed scrolling, and artist profile navigation.

### Notes
- Searching partial artist name (3 chars) — returns results ✅
- Searching with all caps — case insensitive ✅
- Searching with leading/trailing spaces — trimmed ✅
- Rapid typing "a", "ab", "abc" — single request after debounce ✅
- Feed: swipe very fast through 10 tracks — no memory issues ✅
- Feed: audio correctly switches when page changes ✅
- Artist profile from custom artist (UUID) — loads correctly ✅
- Audius artist profile — bio and follower count shown ✅
- Tapping "All Tracks" on artist profile — opens full track list ✅

### Bugs Found
- **BUG-005** — Feed loading spinner stuck on slow connection (fixed with timeout)
- **BUG-011** — Track info sheet hangs for custom tracks (fixed with isCustom check)

---

## Session 5 — Admin Panel

**Date:** July 2026  
**Duration:** 35 minutes  
**Focus:** CRUD operations, file upload, moderation  
**Tester:** Miroslav Gilevich

### Charter
Test admin panel create/edit/delete flows, file uploads, and moderation features.

### Notes
- Creating artist with Cyrillic name — works ✅
- Uploading Cyrillic filename audio — FAILED (BUG-004, fixed)
- Uploading large image (5MB) — takes ~3s, progress bar shown ✅
- Deleting user with active reports — cascade works ✅
- Banning user — user sees ban notice in app on next open ✅
- Appeal from banned user — appears in Appeals tab ✅
- Dashboard stats — match actual DB COUNT queries ✅
- Filtering users by name in admin — search works ✅

### Bugs Found
- **BUG-004** — Cyrillic filename upload fails (fixed with sanitizeFileName)
- Admin session doesn't expire — password re-entry not required after browser close
