# Test Cases — Reviews & Ratings

**Module:** Reviews & Ratings  
**Total:** 20 test cases

---

## Rating (5 Criteria)

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-066 | Submit rating with all 5 criteria filled | Critical | Track opened, user logged in | 1. Tap pencil icon on track 2. Set all 5 sliders 3. Tap "Save Rating" | Rating saved, average score shown in circle | PASS |
| TC-067 | Average score calculated correctly | High | Rating submitted | 1. Set scores: 8, 6, 7, 9, 5 2. Save | Average shown: 7.0 | PASS |
| TC-068 | Cannot save rating without all 5 criteria | High | Rating sheet open | 1. Set only 3 sliders 2. Tap Save | Button disabled or shows "Rate all criteria" | PASS |
| TC-069 | Edit existing rating | High | Rating already saved | 1. Tap pencil icon 2. Change one slider 3. Save | Rating updated, new average shown | PASS |
| TC-070 | Rating persists after app restart | Critical | Rating submitted | 1. Close app 2. Reopen 3. Find same track | Rating value still shown correctly | PASS |
| TC-071 | Rating visible on Reviews screen | High | Rating submitted with review text | 1. Open Reviews screen for rated track | Rating card visible with username and score | PASS |

---

## Reviews (Text)

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-072 | Submit review text after rating | High | Rating saved | 1. Type review text 2. Tap send button | Review saved, appears in list | PASS |
| TC-073 | Review requires rating first | Medium | No rating set | 1. Type review 2. Tap send | Prompt: "You need to set a rating first" | PASS |
| TC-074 | Review shows immediately after submit | High | TC-072 done | 1. Submit review | Review appears in list without reload | PASS |
| TC-075 | Reviews sorted by reputation | Medium | Multiple reviews exist | 1. Open Reviews screen | Reviews sorted highest reputation first | PASS |
| TC-076 | Own review username highlighted purple | Medium | Own review in list | 1. Open Reviews screen | Own username is purple; others grey | PASS |
| TC-077 | Tap avatar on other's review navigates to profile | Medium | Other user's review visible | 1. Long press on other's review | Profile navigation triggered | PASS |

---

## Reputation Voting

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-078 | Upvote review increases reputation | Critical | Other user's review exists | 1. Tap ↑ on a review | Counter increases by +1, button turns green | PASS |
| TC-079 | Downvote review decreases reputation | Critical | Other user's review exists | 1. Tap ↓ on a review | Counter decreases by -1, button turns red | PASS |
| TC-080 | Reputation persists after app restart | Critical | Vote submitted | 1. Close app 2. Reopen 3. Find same review | Vote state preserved, correct reputation shown | PASS |
| TC-081 | Cannot vote on own review | High | Viewing own review | 1. Open own review | Vote buttons are greyed out and non-interactive | PASS |
| TC-082 | Switch vote from up to down | Medium | Upvote submitted | 1. Tap ↓ on same review | Vote changes to -1, counter updates correctly | PASS |

---

## Reports

| ID | Title | Priority | Preconditions | Steps | Expected Result | Status |
|----|-------|----------|---------------|-------|-----------------|--------|
| TC-083 | Long press on review opens report dialog | Medium | Other's review visible | 1. Long press on review | Report dialog appears with reason options | PASS |
| TC-084 | Submit report with selected reason | Medium | Report dialog open | 1. Select reason 2. Tap report | "Report submitted" confirmation shown | PASS |
| TC-085 | Cannot report own review | Medium | Own review visible | 1. Long press on own review | No report dialog shown | PASS |
