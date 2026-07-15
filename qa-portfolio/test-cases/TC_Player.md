# Test Cases — Music Player

**Module:** Player  
**Total:** 25 test cases

---

## Basic Playback

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-021 | Play track from search results | Critical | User logged in, track found | 1. Search for a track 2. Tap track name | Full-screen player opens, track starts playing, waveform animates | PASS |
| TC-022 | Pause playback | Critical | Track is playing | 1. Tap Pause button | Playback pauses, button changes to Play icon | PASS |
| TC-023 | Resume playback | Critical | Track is paused | 1. Tap Play button | Playback resumes from paused position | PASS |
| TC-024 | Seek via waveform progress bar | High | Track is playing | 1. Tap on 70% of progress bar | Playback jumps to ~70% of track duration | PASS |
| TC-025 | Next track via button | High | Playlist has 2+ tracks | 1. Tap Next button | Next track starts playing, artwork and title update | PASS |
| TC-026 | Previous track via button | High | Playlist has 2+ tracks, 2nd track playing | 1. Tap Previous button | Previous track starts playing | PASS |
| TC-027 | Next track via horizontal swipe right | Medium | Player is open | 1. Swipe left on album art | Next track loads | PASS |
| TC-028 | Previous track via horizontal swipe left | Medium | Player is open, 2+ tracks | 1. Swipe right on album art | Previous track loads | PASS |
| TC-029 | Close player via swipe down | Medium | Player is open | 1. Swipe down on player | Player closes, returns to previous screen | PASS |
| TC-030 | Mini-player visible when player is minimized | High | Track is playing | 1. Close player | Mini-player shown at bottom with track info | PASS |

---

## Album Art & HD Cover

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-031 | HD album art loads progressively | Medium | Track with artwork | 1. Open player for track with artwork | LQ shown instantly, HD loads and fades in smoothly | PASS |
| TC-032 | Track without artwork shows placeholder | Low | Track with no cover | 1. Open player for track without cover | Music note icon shown as placeholder | PASS |

---

## Notification & Background

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-033 | Media notification shown during playback | High | Track is playing | 1. Minimize app | Notification appears with track name, artist, Play/Pause/Next buttons | PASS |
| TC-034 | Pause from notification | High | Track playing, app minimized | 1. Tap Pause in notification | Playback pauses | PASS |
| TC-035 | Music continues when app is in background | Critical | Track is playing | 1. Press Home button | Music continues playing | PASS |

---

## Sleep Timer

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-036 | Start sleep timer | Medium | Track playing, Settings open | 1. Go to Settings → Sleep Timer 2. Set 1 minute 3. Tap Start | Timer shows countdown, music stops after 1 min | PASS |
| TC-037 | Cancel sleep timer | Medium | Sleep timer active | 1. Go to Settings → Sleep Timer 2. Tap Cancel | Timer cancelled, music continues | PASS |
| TC-038 | Sleep timer countdown displayed | Low | Sleep timer active | 1. Open sleep timer card | Live countdown shown (ticks every second) | PASS |

---

## Equalizer & Playback Speed

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-039 | Enable equalizer | Medium | Settings → Equalizer | 1. Toggle equalizer on | Band sliders become active, audio changes | PASS |
| TC-040 | Apply equalizer preset | Medium | Equalizer enabled | 1. Select "Rock" preset | Band sliders update to preset values | PASS |
| TC-041 | Change playback speed to 1.5x | Medium | Track is playing | 1. Settings → Playback Speed 2. Select 1.5x | Track plays at 1.5x speed | PASS |
| TC-042 | Playback speed resets default on logout | Low | Speed changed to 2x | 1. Logout 2. Login | Speed returns to 1x | FAIL |

---

## Floating Comments

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-043 | Floating comments appear on player | Low | Track has comments | 1. Open player for commented track | Comments float across album art periodically | PASS |
| TC-044 | Disable floating comments in settings | Low | Floating comments enabled | 1. Settings → disable floating comments | No comments shown on player | PASS |
| TC-045 | Floating comments hidden when no comments exist | Low | Track has 0 comments | 1. Open player | No floating comments shown | PASS |
