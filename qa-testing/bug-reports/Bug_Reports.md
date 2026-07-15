# Bug Reports — LumiSound

**Total Bugs:** 23  
**Critical:** 2 | **Major:** 7 | **Minor:** 10 | **Trivial:** 4

---

## BUG-001 — Player progress bar position not restored after app restart

| Field | Value |
|-------|-------|
| **ID** | BUG-001 |
| **Title** | Player progress bar position not restored after app restart |
| **Severity** | Major |
| **Priority** | High |
| **Module** | Player |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Start playing a track
2. Seek to ~60% position
3. Close app completely (kill from recents)
4. Reopen app

**Expected Result:** Track resumes from ~60% position  
**Actual Result:** Track starts from the beginning (0%)  
**Fix:** Added `DiskCache.saveLastTrack()` call in `PlayerViewModel` on track change

---

## BUG-002 — Reputation counter shows 0 after voting despite vote being saved

| Field | Value |
|-------|-------|
| **ID** | BUG-002 |
| **Title** | Review reputation not updated after voting |
| **Severity** | Critical |
| **Priority** | Critical |
| **Module** | Reviews |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Open any track's reviews screen
2. Tap ↑ on someone's review
3. Close app
4. Reopen, find the same review

**Expected Result:** Reputation shows +1  
**Actual Result:** Reputation shows 0  
**Root Cause:** RLS policy `tr_update` prevented updating `reputation` on other user's rows. `PATCH` was silently ignored.  
**Fix:** Created `SECURITY DEFINER` RPC function `update_review_reputation(p_rating_id UUID)` that bypasses RLS and recalculates `SUM(vote)` from `review_votes` table.

---

## BUG-003 — Track audio/visual desync when using "Next" in queue

| Field | Value |
|-------|-------|
| **ID** | BUG-003 |
| **Title** | Audio plays from Track A while UI shows Track B |
| **Severity** | Critical |
| **Priority** | Critical |
| **Module** | Player |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Play a track from a playlist
2. Add more tracks to queue (appendToQueue)
3. Tap "Next" repeatedly

**Expected Result:** UI and audio match the same track  
**Actual Result:** UI shows Track B but audio plays Track A  
**Root Cause:** `onMediaItemTransition` was triggered by `PLAYLIST_CHANGED` reason when appending tracks, causing premature visual update.  
**Fix:** Added filter to ignore `MEDIA_ITEM_TRANSITION_REASON_PLAYLIST_CHANGED`. Used `setIndexOnly()` instead of `setPlaylist()` for next/prev navigation.

---

## BUG-004 — Custom track cover and audio URLs are null after creation

| Field | Value |
|-------|-------|
| **ID** | BUG-004 |
| **Title** | Admin-created track has null audio_url and cover_url |
| **Severity** | Major |
| **Priority** | High |
| **Module** | Admin Panel |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Open admin panel
2. Create new track with Cyrillic filename (e.g. "ПАДШИЙТВОРЕЦ.mp3")
3. Check database

**Expected Result:** `audio_url` contains public Storage URL  
**Actual Result:** `audio_url = null`  
**Root Cause:** Supabase Storage rejected file path with Cyrillic characters (`Invalid key` error). Upload silently failed.  
**Fix:** Added `sanitizeFileName()` in `admin/app.js` — replaces original filename with `timestamp + extension` only.

---

## BUG-005 — Feed loading spinner stuck indefinitely when Audius API is slow

| Field | Value |
|-------|-------|
| **ID** | BUG-005 |
| **Title** | Discovery feed shows infinite loading spinner |
| **Severity** | Major |
| **Priority** | High |
| **Module** | Search / Feed |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Open Search tab with slow internet
2. Observe feed

**Expected Result:** Loading times out after ~12s, "Refresh" button shown  
**Actual Result:** Spinner shown indefinitely, tabs "Recommendations" / "For You" unclickable  
**Root Cause:** `loadFeeds()` awaited both API calls sequentially without timeout. `_feedLoading` never set to `false`.  
**Fix:** Wrapped calls in `withTimeoutOrNull(12_000L)`, ran them via `async/await` in parallel, moved `HorizontalPager` outside `if (isLoading)` block.

---

## BUG-006 — Average rating not shown in TikTok feed card

| Field | Value |
|-------|-------|
| **ID** | BUG-006 |
| **Title** | Average rating always shows 0 in feed stats |
| **Severity** | Major |
| **Priority** | Medium |
| **Module** | Feed / Ratings |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Rate a track
2. Open TikTok feed with the same track

**Expected Result:** Rating badge shows average score  
**Actual Result:** Badge shows 0 or empty  
**Root Cause:** `getTrackAverageRating` deserialized `rating_count` field, but the view `track_ratings_avg` returns `review_count`. Field was always 0.  
**Fix:** Added `review_count` field to `ViewRow` and used `if (ratingCount > 0) ratingCount else reviewCount`.

---

## BUG-007 — Sleep timer icon not clickable

| Field | Value |
|-------|-------|
| **ID** | BUG-007 |
| **Title** | Sleep timer clock icon in player does not respond to tap |
| **Severity** | Minor |
| **Priority** | Medium |
| **Module** | Settings / Player |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Start sleep timer
2. In player, tap the clock icon

**Expected Result:** Dialog shows remaining time  
**Actual Result:** No response  
**Root Cause:** `Modifier.then(if (...) Modifier.clickable {...} else Modifier)` — conditional clickable removed the hit area entirely.  
**Fix:** Applied `clickable` unconditionally, moved condition inside the click handler.

---

## BUG-008 — Settings "About" screen: back gesture returns to Profile instead of Settings

| Field | Value |
|-------|-------|
| **ID** | BUG-008 |
| **Title** | Android back gesture from About screen navigates to Profile, not Settings |
| **Severity** | Minor |
| **Priority** | Medium |
| **Module** | Settings / Navigation |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Open Settings
2. Tap "About"
3. Press Android back gesture

**Expected Result:** Returns to Settings  
**Actual Result:** Returns to Profile  
**Root Cause:** `AboutScreen` was rendered inside `SettingsScreen` via `if (showAboutScreen) { ... return }`. Android `BackHandler` was not registered.  
**Fix:** Added `BackHandler { showAboutScreen = false }` before rendering `AboutScreen`.

---

## BUG-009 — Logout does not stop music

| Field | Value |
|-------|-------|
| **ID** | BUG-009 |
| **Title** | Music continues playing after logout |
| **Severity** | Major |
| **Priority** | High |
| **Module** | Settings / Player |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Start a track
2. Go to Settings → Logout

**Expected Result:** Music stops, notification dismissed  
**Actual Result:** Music continues playing in background  
**Fix:** Added `audioPlayerService.stop()`, `cancelSleepTimer()`, `dismissNotification()`, `playerStateHolder.setPlaylist(emptyList())` to `SettingsViewModel.logout()`.

---

## BUG-010 — Review votes not loaded on screen open

| Field | Value |
|-------|-------|
| **ID** | BUG-010 |
| **Title** | Previously voted reviews show no vote state after reopening screen |
| **Severity** | Major |
| **Priority** | High |
| **Module** | Reviews |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Vote ↑ on a review
2. Close reviews screen
3. Reopen same track's reviews

**Expected Result:** ↑ button is green, counter shows +1  
**Actual Result:** ↑ button is grey, counter shows 0  
**Root Cause:** `loadForTrack()` did not load `myVotes` — `Map<String, Int>` was always empty on open.  
**Fix:** Added `getMyVotesForReviews()` batch call in `loadForTrack()` after loading reviews.

---

## BUG-011 — Player info sheet (⋮) hangs for custom tracks

| Field | Value |
|-------|-------|
| **ID** | BUG-011 |
| **Title** | TrackInfoSheet shows infinite loading for custom tracks |
| **Severity** | Minor |
| **Priority** | Medium |
| **Module** | Player |
| **Status** | Fixed |

**Steps to Reproduce:**
1. Play a custom track (added via admin panel)
2. Tap ⋮ (more options)

**Expected Result:** Track info shown instantly  
**Actual Result:** Spinner shown indefinitely  
**Root Cause:** `TrackInfoSheet` called `audiusApi.getTrackById("custom_xxx")` — Audius doesn't know this ID, request hung or returned error.  
**Fix:** Added `val isCustom = track.id.startsWith("custom_")` check; skips Audius API call for custom tracks.

---

## BUG-012 — App icon change requires app restart

| Field | Value |
|-------|-------|
| **ID** | BUG-012 |
| **Title** | Selected app icon not visible on home screen until app restart |
| **Severity** | Trivial |
| **Priority** | Low |
| **Module** | Settings |
| **Status** | Known / Won't Fix |

**Steps to Reproduce:**
1. Go to Settings → App Icon
2. Select "Blue"
3. Check home screen immediately

**Expected Result:** Icon changes immediately  
**Actual Result:** Old icon shown until app restart  
**Note:** This is Android system limitation — icon alias change requires app to be killed.

---

## BUG-013 — Profile picture not updating on review cards after avatar change

| Field | Value |
|-------|-------|
| **ID** | BUG-013 |
| **Title** | Old avatar shown on review cards after user changes avatar |
| **Severity** | Minor |
| **Priority** | Low |
| **Module** | Profile / Reviews |
| **Status** | Open |

**Steps to Reproduce:**
1. User changes avatar
2. Existing reviews still show old avatar

**Expected Result:** Updated avatar shown  
**Actual Result:** Old avatar from `user_avatar_url` field in `track_ratings` shown  
**Note:** `track_ratings.user_avatar_url` is only updated when user writes a new review, not when avatar changes.

---

## BUG-014 — Playback speed setting resets to 1x after logout

| Field | Value |
|-------|-------|
| **ID** | BUG-014 |
| **Title** | Playback speed resets to 1x after logout and re-login |
| **Severity** | Minor |
| **Priority** | Low |
| **Module** | Settings / Player |
| **Status** | Open |

**Steps to Reproduce:**
1. Set playback speed to 1.5x
2. Logout
3. Login again

**Expected Result:** Speed setting preserved at 1.5x  
**Actual Result:** Speed reset to 1x  
**Note:** Speed is stored in `SessionManager`, which is cleared on logout.

---

## BUG-015 to BUG-023 — Minor & Trivial Issues

| ID | Title | Severity | Status |
|----|-------|----------|--------|
| BUG-015 | Search results briefly show previous query when typing fast | Minor | Fixed |
| BUG-016 | Floating comments overlap bottom controls in landscape | Minor | Open |
| BUG-017 | Artist profile shows "Not found" for custom artist if UUID not detected | Major | Fixed |
| BUG-018 | Registration form doesn't scroll to error field | Trivial | Open |
| BUG-019 | Admin panel: track list shows placeholder instead of cover if URL invalid | Minor | Open |
| BUG-020 | Synthesis invite code not copyable on some Android versions | Minor | Open |
| BUG-021 | Settings equalizer screen back button inconsistent | Trivial | Fixed |
| BUG-022 | Dark theme primary color shown as grey in some components | Trivial | Open |
| BUG-023 | Profile "About app" copyright year hardcoded as 2025 | Trivial | Open |
