# Test Plan — LumiSound Android Application

**Document ID:** TP-001  
**Version:** 1.0  
**Date:** July 2026  
**Author:** Miroslav Gilevich  
**Status:** Approved

---

## 1. Objective

The objective of this test plan is to verify that the LumiSound Android application functions correctly, meets the specified requirements, and provides a stable user experience across core features: authentication, music playback, search, ratings, playlists, and the admin panel.

---

## 2. Scope

### In Scope
- Authentication (registration, login, email confirmation, password reset)
- Music player (playback, controls, queue, sleep timer, equalizer)
- TikTok-style discovery feed (Recommendations, For You)
- Search (tracks, artists, custom content)
- Reviews and ratings (5-criteria scoring, reviews, reputation voting)
- Comments (write, delete, report)
- Playlists (create, edit, tracks, visibility)
- Synthesis sessions (collaborative playlist via invite code)
- User profile (edit, avatar, stats, favorites)
- Settings (theme, equalizer, speed, icons, cache)
- Admin panel (users, artists, tracks, reports, bans, appeals)
- Supabase REST API
- PostgreSQL database validation via SQL

### Out of Scope
- Performance / load testing
- Automated UI testing
- Security penetration testing
- iOS version (Android only)

---

## 3. Test Environment

| Parameter | Value |
|-----------|-------|
| Device | Real Android device (Android 12+) |
| Min SDK | Android 7.0 (API 24) |
| Target SDK | Android 15 (API 36) |
| Backend | Supabase (PostgreSQL) |
| Music API | Audius API |
| Network | WiFi + Mobile data |
| Build | Debug APK |
| Tools | Android Studio, Postman, Supabase Dashboard |

---

## 4. Entry Criteria

- Debug APK is installed on the test device
- Supabase database is accessible
- Audius API is available
- Test account credentials are prepared
- Admin panel is accessible via browser

---

## 5. Exit Criteria

- All Critical and Major test cases are executed
- No open Critical bugs
- No more than 2 open Major bugs
- Test Summary Report is complete

---

## 6. Test Types

| Type | Description |
|------|-------------|
| Functional | Verify features work as specified |
| Negative | Test invalid inputs and error handling |
| Exploratory | Unscripted testing to find unexpected defects |
| Regression | Verify that bug fixes don't break existing features |
| API | Validate REST API endpoints via Postman |
| Database | Validate data integrity via SQL queries |

---

## 7. Risks

| Risk | Mitigation |
|------|-----------|
| Audius API unavailability | Test with cached data; note in report |
| Supabase rate limits | Spread API tests over time |
| Device-specific UI issues | Test on multiple screen sizes if possible |
| Network instability | Test both online and offline scenarios |

---

## 8. Test Deliverables

- Test Plan (this document)
- Test Cases (per module)
- Bug Reports
- Checklists
- API Test Collection (Postman)
- SQL Query Scripts
- Exploratory Testing Sessions
- Test Summary Report

---

## 9. Schedule

| Phase | Activity |
|-------|---------|
| Week 1 | Test plan, test case design |
| Week 2 | Test execution (Auth, Player, Search) |
| Week 3 | Test execution (Reviews, Playlists, Profile, Admin) |
| Week 4 | API/SQL testing, exploratory, bug reporting, summary |
