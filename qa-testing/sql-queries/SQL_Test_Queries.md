# SQL Test Queries — LumiSound Database

**Database:** PostgreSQL (Supabase)  
**Purpose:** Data integrity validation and test support queries

---

## User Queries

### SQL-001 — Find all registered users
```sql
SELECT id, username, email, created_at
FROM profiles
ORDER BY created_at DESC;
```
**Purpose:** Verify registration creates profile record

---

### SQL-002 — Find duplicate emails
```sql
SELECT email, COUNT(*) as cnt
FROM profiles
GROUP BY email
HAVING COUNT(*) > 1;
```
**Expected:** 0 rows (no duplicates)

---

### SQL-003 — Find users without profiles (auth.users with no profiles row)
```sql
SELECT au.id, au.email
FROM auth.users au
LEFT JOIN profiles p ON p.id = au.id
WHERE p.id IS NULL;
```
**Purpose:** Detect registration edge cases

---

## Track Ratings Queries

### SQL-004 — Get all ratings for a specific track with username
```sql
SELECT 
    tr.id,
    tr.audius_track_id,
    p.username,
    tr.rhyme_score,
    tr.imagery_score,
    tr.structure_score,
    tr.charisma_score,
    tr.atmosphere_score,
    tr.overall_score,
    tr.reputation,
    tr.created_at
FROM track_ratings tr
JOIN profiles p ON p.id = tr.user_id
WHERE tr.audius_track_id = 'YOUR_TRACK_ID'
ORDER BY tr.reputation DESC;
```
**Purpose:** Verify ratings are saved and sorted correctly

---

### SQL-005 — Verify reputation matches sum of votes
```sql
SELECT 
    tr.id,
    tr.reputation AS stored_reputation,
    COALESCE(SUM(rv.vote), 0) AS calculated_reputation,
    CASE WHEN tr.reputation = COALESCE(SUM(rv.vote), 0) 
         THEN 'OK' ELSE 'MISMATCH' END AS status
FROM track_ratings tr
LEFT JOIN review_votes rv ON rv.rating_id = tr.id
GROUP BY tr.id, tr.reputation;
```
**Expected:** All rows show `status = 'OK'`

---

### SQL-006 — Find ratings with incomplete criteria (< 5 scores)
```sql
SELECT id, user_id, audius_track_id
FROM track_ratings
WHERE rhyme_score IS NULL
   OR imagery_score IS NULL
   OR structure_score IS NULL
   OR charisma_score IS NULL
   OR atmosphere_score IS NULL;
```
**Purpose:** Verify constraint works correctly

---

## Playlists Queries

### SQL-007 — Count tracks per playlist
```sql
SELECT 
    pl.id,
    pl.name,
    pl.track_count AS stored_count,
    COUNT(pt.id) AS actual_count,
    CASE WHEN pl.track_count = COUNT(pt.id) 
         THEN 'OK' ELSE 'MISMATCH' END AS status
FROM playlists pl
LEFT JOIN playlist_tracks pt ON pt.playlist_id = pl.id
GROUP BY pl.id, pl.name, pl.track_count;
```
**Expected:** All `status = 'OK'`

---

### SQL-008 — Find public playlists
```sql
SELECT id, name, user_id, track_count, created_at
FROM playlists
WHERE is_public = true
ORDER BY created_at DESC;
```

---

## Review Votes Queries

### SQL-009 — Get all votes by a specific user
```sql
SELECT rv.rating_id, rv.vote, tr.overall_score, p.username
FROM review_votes rv
JOIN track_ratings tr ON tr.id = rv.rating_id
JOIN profiles p ON p.id = tr.user_id
WHERE rv.user_id = 'YOUR_USER_ID';
```

---

### SQL-010 — Find reviews with highest reputation
```sql
SELECT 
    tr.id,
    p.username,
    tr.track_title,
    tr.overall_score,
    tr.reputation,
    LEFT(tr.review, 50) AS review_preview
FROM track_ratings tr
JOIN profiles p ON p.id = tr.user_id
WHERE tr.review IS NOT NULL
ORDER BY tr.reputation DESC
LIMIT 10;
```

---

## Reports & Moderation Queries

### SQL-011 — Get all unprocessed reports
```sql
SELECT 
    r.id,
    r.target_type,
    r.reason,
    p.username AS reporter,
    r.target_username,
    r.created_at
FROM reports r
JOIN profiles p ON p.id = r.reporter_id
ORDER BY r.created_at DESC;
```

---

### SQL-012 — Sync all reputation values from votes (maintenance)
```sql
UPDATE track_ratings tr
SET reputation = (
    SELECT COALESCE(SUM(rv.vote), 0)
    FROM review_votes rv
    WHERE rv.rating_id = tr.id
);
```
**Purpose:** Used to fix reputation after migration / bug fix
