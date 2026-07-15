# API Testing — LumiSound (Supabase REST)

**Tool:** Postman  
**Base URL:** `https://dmwnegtvotnrajzpyfad.supabase.co/rest/v1`  
**Auth:** Bearer Token (JWT from Supabase Auth)

---

## Authentication Endpoints

### AT-001 — POST /auth/v1/token (Login)

**Request:**
```json
POST /auth/v1/token?grant_type=password
{
  "email": "test@test.com",
  "password": "Test1234"
}
```
**Expected:** 200 OK, `access_token` in response  
**Actual:** ✅ 200 OK — token received  
**Notes:** Verified `refresh_token` and `expires_in` fields present

---

### AT-002 — POST /auth/v1/token (Wrong Password)

**Request:**
```json
{
  "email": "test@test.com",
  "password": "wrongpassword"
}
```
**Expected:** 400, `error: "invalid_grant"`  
**Actual:** ✅ 400 Bad Request — correct error code

---

### AT-003 — POST /auth/v1/token (Invalid Email)

**Expected:** 422, error about email format  
**Actual:** ✅ 422 Unprocessable Entity

---

### AT-004 — GET /auth/v1/user (Valid Token)

**Expected:** 200, user object with id and email  
**Actual:** ✅ 200 OK — user data returned

---

### AT-005 — GET /auth/v1/user (Invalid Token)

**Expected:** 401 Unauthorized  
**Actual:** ✅ 401 Unauthorized

---

## Profiles

### PR-001 — GET /rest/v1/profiles?id=eq.{userId}

**Expected:** 200, array with 1 profile object  
**Actual:** ✅ 200 OK

---

### PR-002 — PATCH /rest/v1/profiles?id=eq.{userId}

**Body:** `{"username": "NewName"}`  
**Expected:** 204 No Content  
**Actual:** ✅ 204 No Content — verified in DB

---

### PR-003 — PATCH profile with wrong user token (RLS test)

**Expected:** 0 rows updated (RLS blocks it)  
**Actual:** ✅ 204 but 0 rows affected — RLS working correctly

---

## Track Ratings

### TR-001 — POST /rest/v1/track_ratings (Upsert rating)

**Headers:** `Prefer: resolution=merge-duplicates`  
**Body:**
```json
{
  "audius_track_id": "abc123",
  "rhyme_score": 8,
  "imagery_score": 7,
  "structure_score": 9,
  "charisma_score": 6,
  "atmosphere_score": 8,
  "track_title": "Test Track",
  "track_artist": "Test Artist"
}
```
**Expected:** 201 Created  
**Actual:** ✅ 201 Created

---

### TR-002 — GET /rest/v1/track_ratings?audius_track_id=eq.{id}

**Expected:** 200, array of ratings sorted by reputation  
**Actual:** ✅ 200 OK — ratings returned

---

### TR-003 — POST /rest/v1/review_votes (Vote)

**Body:** `[{"user_id": "...", "rating_id": "...", "vote": 1}]`  
**Prefer:** `resolution=merge-duplicates`  
**Expected:** 201 Created  
**Actual:** ✅ 201 Created

---

### TR-004 — POST /rest/v1/rpc/update_review_reputation

**Body:** `{"p_rating_id": "..."}`  
**Expected:** 200 OK, reputation updated in DB  
**Actual:** ✅ 200 OK — verified via SQL: `SELECT reputation FROM track_ratings WHERE id = '...'`

---

## Playlists

### PL-001 — POST /rest/v1/playlists (Create playlist)

**Expected:** 201, playlist object returned  
**Actual:** ✅ 201 Created

---

### PL-002 — DELETE /rest/v1/playlists?id=eq.{id}

**Expected:** 204 No Content  
**Actual:** ✅ 204 No Content

---

### PL-003 — DELETE playlist owned by other user (RLS test)

**Expected:** 204 but 0 rows deleted  
**Actual:** ✅ Correctly blocked by RLS

---

## Custom Tracks (Admin)

### CT-001 — GET /rest/v1/custom_tracks?title=ilike.*test*

**Expected:** 200, matching tracks  
**Actual:** ✅ 200 OK

---

### CT-002 — GET /rest/v1/custom_artists?name=ilike.*Lumi*

**Expected:** 200, matching artists  
**Actual:** ✅ 200 OK

---

## Reports

### RP-001 — POST /rest/v1/reports (Submit report)

**Expected:** 201 Created  
**Actual:** ✅ 201 Created

---

### RP-002 — Anonymous user submitting report (no token)

**Expected:** 401 or RLS blocks insert  
**Actual:** ✅ 401 Unauthorized

---

## Summary

| Category | Total | Passed | Failed |
|----------|-------|--------|--------|
| Authentication | 5 | 5 | 0 |
| Profiles | 3 | 3 | 0 |
| Track Ratings | 4 | 4 | 0 |
| Playlists | 3 | 3 | 0 |
| Custom Content | 2 | 2 | 0 |
| Reports | 2 | 2 | 0 |
| **Total** | **19** | **19** | **0** |
