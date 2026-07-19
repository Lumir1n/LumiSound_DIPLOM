<div align="center">

# 🎵 LumiSound

**Android music streaming app with social review system**

[![Kotlin](https://img.shields.io/badge/Kotlin-1.9-7F52FF?logo=kotlin&logoColor=white)](https://kotlinlang.org)
[![Jetpack Compose](https://img.shields.io/badge/Jetpack%20Compose-UI-4285F4?logo=jetpackcompose&logoColor=white)](https://developer.android.com/jetpack/compose)
[![Android](https://img.shields.io/badge/Android-24%2B-3DDC84?logo=android&logoColor=white)](https://android.com)
[![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?logo=supabase&logoColor=white)](https://supabase.com)
[![Audius](https://img.shields.io/badge/Audius-API-CC0000?logo=audius&logoColor=white)](https://audius.co)

*Listen. Rate. Discover. Together.*

</div>

---

## 📱 About

LumiSound is a full-featured Android music streaming application that goes beyond passive listening. Users can rate tracks across **5 detailed criteria**, write reviews, vote on others' opinions, create playlists, and discover new music through a TikTok-style feed — all powered by the open **Audius API** and **Supabase** backend.

Built as a diploma project, LumiSound represents a complete production-grade application: ~**25,000 lines of Kotlin**, 17+ screens, a web admin panel, and a full social layer around music.

---

## ✨ Features

### 🎵 Music
- Full-screen player with **waveform progress bar**, HD cover art with LQ→HD progressive loading
- Background playback via foreground service with media notification controls
- ExoPlayer-powered queue, seek, next/previous, horizontal swipe between tracks
- TikTok-style vertical discovery feed with **Recommendations** and **For You** tabs
- Sleep timer, equalizer with presets, playback speed, volume normalization

### ⭐ Social & Reviews
- Rate tracks across **5 criteria**: Rhymes/Imagery, Structure/Rhythm, Style Execution, Individuality, Atmosphere
- Write and read full-text reviews
- **Reputation voting system** (↑/↓) with server-side persistence via PostgreSQL RPC
- Comments with floating display on the player screen
- Report system with admin moderation and ban/appeal workflow

### 📋 Playlists
- Create, edit, manage playlists with custom cover images
- **Synthesis sessions** — collaborative playlist creation with a friend via invite code
- Like and discover public playlists

### 👤 Profile & Settings
- Avatar upload with crop, bio, public/private profile toggle
- Listening history, favorite tracks & artists sorted by play count
- Theme: dark / light / system
- **4 app icon variants** (black, white, pink, blue)
- Two-level cache: in-memory (StateFlow) + disk cache

### 🛡 Admin Panel (Web)
- Separate web app (HTML/CSS/JS + Supabase JS)
- CRUD for users, custom artists, tracks (with audio/cover upload)
- Reports, bans, appeals management
- Dashboard with live stats

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Kotlin |
| UI | Jetpack Compose |
| Architecture | MVVM + Repository Pattern |
| DI | Hilt |
| Async | Coroutines + Flow |
| HTTP | Ktor |
| Audio | ExoPlayer (Media3) |
| Images | Coil |
| Navigation | Navigation Compose |
| Backend | Supabase (PostgreSQL) |
| Auth | Supabase Auth (JWT + Refresh Token) |
| Music API | Audius API |
| Storage | Supabase Storage |
| Build | Gradle (Kotlin DSL) |

---

## 🏗 Architecture

```
app/
├── data/
│   ├── cache/          # AppDataCache (in-memory), DiskCache
│   ├── local/          # SessionManager, PendingUsernameStore
│   ├── model/          # Track, ...
│   ├── player/         # AudioPlayerService, PlayerStateHolder
│   ├── remote/         # AudiusApiService, SupabaseService
│   └── repository/     # AuthRepository, MusicRepository
├── di/                 # Hilt modules (AppModule, NetworkModule)
├── feature/
│   ├── auth/           # Welcome, Login, Register, EmailVerify, ProfileSetup
│   ├── artist/         # ArtistCardScreen, ArtistProfileViewModel
│   ├── home/           # HomeScreen, PlaylistDetailScreen, SynthesisScreen
│   ├── nowplaying/     # PlayerScreen, NowPlayingScreen, PlayerViewModel
│   ├── ratings/        # RatingsScreen, ReviewScreen, ReviewsScreen
│   ├── profile/        # ProfileScreen, PublicProfileScreen
│   ├── search/         # SearchScreen (TikTok feed), SearchViewModel
│   └── settings/       # SettingsScreen, EqualizerScreen, AboutScreen
├── navigation/         # MainNavGraph, SwipeableNavHost
└── ui/theme/           # Color, Theme, ThemeManager
```

The app follows **MVVM** with a clean separation between data sources and UI. All network calls are made through repository interfaces — `AuthRepository` and `MusicRepository` — injected via Hilt.

---

## 🗄 Database (Supabase / PostgreSQL)

Key tables: `profiles`, `track_ratings`, `track_comments`, `review_votes`, `playlists`, `playlist_tracks`, `favorite_tracks`, `favorite_artists`, `track_history`, `synthesis_sessions`, `reports`, `user_bans`, `ban_appeals`, `custom_artists`, `custom_tracks`.

All tables have **Row Level Security (RLS)** policies. Sensitive operations (e.g. updating `reputation` across users) use **SECURITY DEFINER** PostgreSQL functions to bypass RLS safely.

---

## 📊 Project Stats

| Metric | Value |
|--------|-------|
| Lines of Kotlin code | ~25,000 |
| Screens | 17+ |
| DB tables | 22 |
| API endpoints | 40+ (Supabase REST) |
| External APIs | Audius API |

---

## 🚀 Build & Run

1. Clone the repository
2. Create `local.properties` in project root:
```properties
SUPABASE_URL=your_supabase_url
SUPABASE_ANON_KEY=your_supabase_anon_key
```
3. Open in Android Studio and run on device (minSdk 24)

> **Note:** The app requires a configured Supabase project with the matching database schema.

---

## 📁 Repository Structure

```
LumiSound_DIPLOM/
├── app/                    # Android application source code
├── admin/                  # Web admin panel (HTML/CSS/JS)
├── DOC/                    # Project documentation
├── EXE/                    # Release APK
└── GRAPH/                  # Graphic materials, presentation
```

---

## 🔗 Related

[![QA Portfolio](https://img.shields.io/badge/QA%20Testing-Portfolio-blue?logo=github)](https://github.com/Lumir1n/LumiSound-QA-Testing)

---

## 👤 Author

**Miroslav Gilevich**  
GitHub: [@Lumir1n](https://github.com/Lumir1n)
