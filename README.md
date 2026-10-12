# Cricket Match Scheduler

A web application for organising cricket tournaments — manage teams, auto-generate match slots, and book matches — all from a single page.

**Live app:** https://cricket-scheduler-771bd.web.app

---

## Features

### For Tournament Owners
- Create and delete tournaments
- Assign organizers to tournaments
- Full visibility across all tournaments and teams

### For Organizers
- Add teams with captain details
- **Auto-generate match slots** — pick multiple dates, set a start time, end time, match duration, and break between matches; all slots are created automatically
- Book matches into any free slot, even if no teams have marked availability
- Schedule custom one-off matches at any time
- View the full match schedule in a sortable table

### For Captains
- Mark team availability for specific dates and time slots
- View their team's upcoming matches

### For Players
- View their own busy/unavailable slots

---

## How It Works

### Authentication
- Sign in with **Google** or **Email & Password**
- Roles are assigned per user: `owner`, `organizer`, `captain`, `player`
- Session automatically expires after **1 hour of inactivity** (5-minute warning shown before logout)

### Role-Based Navigation
Each role sees a different tab set after login:

| Role | Tabs |
|------|------|
| Owner | Tournaments · Teams · Slots · Book Match · Matches |
| Organizer | Tournaments · Teams · Slots · Book Match · Matches |
| Captain | My Availability · Players |
| Player | My Schedule |

### Slot Generation
1. Go to the **Slots** tab
2. Select one or more dates
3. Set start time, end time, match duration (minutes), and optional break between matches
4. Click **Generate Slots** — all time slots for all selected dates are created in one go

### Booking a Match
- Organizers can book any free slot regardless of team availability
- Choose two teams, a venue, and confirm — the match is saved and appears in the Matches table
- The **Book Match** tab also allows scheduling a custom match at a specific date and time outside of generated slots

### Match Table
The Matches tab shows all scheduled matches in a table with:
- Match number, date, start/end time, duration
- Team A vs Team B
- Venue
- Break time

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Hosting | Firebase Hosting |
| Auth | Firebase Authentication (Google + Email/Password) |
| Database | Cloud Firestore |
| Frontend | Vanilla HTML / CSS / JavaScript (single file) |

No build step — the entire app is `index.html`.

---

## Data Model (Firestore Collections)

| Collection | Purpose |
|------------|---------|
| `tournaments` | Tournament records |
| `teams` | Teams with captain email and player count |
| `users` | User profiles with role |
| `matchSlots` | Auto-generated time slots per tournament |
| `teamSlotAvail` | Captain availability marks |
| `busySlots` | Player unavailability |
| `matches` | Booked/scheduled matches |

---

## Running Locally

No build required. Open `index.html` directly in a browser, or serve it with any static file server:

```bash
npx serve .
```

The app connects to the live Firebase project, so data is shared with the production deployment.

---

## Deployment

```bash
firebase deploy --only hosting
```

Requires [Firebase CLI](https://firebase.google.com/docs/cli) and access to the `cricket-scheduler-771bd` project.
