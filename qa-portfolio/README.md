# 🎵 LumiSound — QA Portfolio

**Manual Testing Portfolio** for the LumiSound Android Application

> LumiSound is a full-featured Android music streaming app with social features: reviews, ratings, playlists, TikTok-style feed, and an admin panel. Built by the same author — which means this QA project is based on **deep knowledge of the architecture, database, API, and business logic**.

---

## 📱 Application Under Test

| Property | Details |
|----------|---------|
| **App Name** | LumiSound |
| **Platform** | Android (minSdk 24, targetSdk 36) |
| **Language** | Kotlin + Jetpack Compose |
| **Architecture** | MVVM + Repository Pattern |
| **Backend** | Supabase (PostgreSQL) |
| **Music API** | Audius API |
| **Source Code** | [LumiSound Repository](https://github.com/Eeer1mald/LumiSound_DIPLOM) |

---

## 🧪 Testing Scope

| Module | Description |
|--------|-------------|
| Authentication | Registration, Login, Email confirmation, Password reset |
| Player | Playback, seek, next/prev, queue, sleep timer |
| Search | Track search, artist search, TikTok feed |
| Reviews & Ratings | 5-criteria rating, reviews, vote system (reputation) |
| Comments | Write, delete, report |
| Playlists | Create, edit, add/remove tracks, visibility |
| Synthesis | Joint playlist session via invite code |
| Profile | Edit, avatar upload, stats |
| Settings | Theme, equalizer, playback speed, cache |
| Admin Panel | Users, artists, tracks, reports, bans, appeals |
| API | Supabase REST API via Postman |
| Database | SQL queries against PostgreSQL (Supabase) |

---

## 🛠 Tools Used

| Tool | Purpose |
|------|---------|
| Android Studio | App installation, logcat, device testing |
| Postman | API testing (Supabase REST) |
| SQL (Supabase Dashboard) | Database queries & validation |
| Git / GitHub | Version control, bug tracking via Issues |
| draw.io | Test flow diagrams |

---

## 📂 Repository Contents

```
qa-portfolio/
├── README.md
├── test-plan/
│   └── Test_Plan.md
├── test-cases/
│   ├── TC_Authentication.md
│   ├── TC_Player.md
│   ├── TC_Search.md
│   ├── TC_Reviews_Ratings.md
│   ├── TC_Playlists.md
│   ├── TC_Profile_Settings.md
│   └── TC_Admin_Panel.md
├── bug-reports/
│   └── Bug_Reports.md
├── checklists/
│   ├── CL_Registration.md
│   └── CL_Regression.md
├── api-testing/
│   └── API_Test_Results.md
├── sql-queries/
│   └── SQL_Test_Queries.md
├── exploratory-testing/
│   └── Exploratory_Sessions.md
└── test-summary/
    └── Test_Summary_Report.md
```

---

## 📊 Statistics

| Artifact | Count |
|----------|-------|
| Test Cases | 145 |
| Bug Reports | 23 |
| Checklists | 9 |
| SQL Queries | 12 |
| API Test Cases | 28 |
| Regression Suites | 3 |

---

## ✅ Execution Results

| Module | Total | Passed | Failed |
|--------|-------|--------|--------|
| Authentication | 20 | 18 | 2 |
| Player | 25 | 23 | 2 |
| Search & Feed | 20 | 19 | 1 |
| Reviews & Ratings | 20 | 18 | 2 |
| Playlists | 20 | 20 | 0 |
| Profile & Settings | 15 | 15 | 0 |
| Admin Panel | 15 | 14 | 1 |
| API Testing | 10 | 9 | 1 |
| **Total** | **145** | **136** | **9** |

---

## 👤 Author

**Miroslav Gilevich** — Junior QA Engineer  
GitHub: [Eeer1mald](https://github.com/Eeer1mald)
