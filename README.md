# Workout Planner

A personalized workout system powered by Claude that acts as your personal trainer. It emails you your daily workout, lets you log sets on your phone, and automatically adjusts your program each week based on your performance.

## How It Works

```
Monday/Wednesday/Friday at 6 AM
  → Gmail draft with today's workout + target weights
  → "Open Workout Logger" button at the top of the email
  → Log weight, reps, RPE after each set on your phone
  → Tap "Email Log" when done

Each night at 10 PM
  → Claude parses any new "Workout Log" emails
  → Updates data/history.json so the dashboard stays fresh on any device

Sunday at 7 PM
  → Claude reviews the week's logs
  → Adjusts weights based on reps and RPE
  → Rotates exercises for variety
  → Writes next week's plan
  → Sends a weekly summary with explanations
```

## Setup

- **Equipment**: Home gym — barbell, power rack with pulley accessory, full dumbbell set, EZ curl bar, pull-up bar, lat bar, rope attachment, leg extension/curl attachment, dip bars
- **Schedule**: 3 lifting days (Mon / Wed / Fri), runs separately on Thursdays
- **Split**: Push / Pull / Legs
- **Session**: ~45 minutes
- **Logger**: https://travis-coder135.github.io/workout-planner/

## Pinned Exercises (The Big 3)

These are always the first exercise on their day and never get swapped out:

| Day | Exercise |
|-----|----------|
| Monday (Push) | Barbell Bench Press |
| Wednesday (Pull) | Barbell Deadlift |
| Friday (Legs) | Barbell Back Squat |

## Goals

Change your training goal anytime via the Settings tab in the logger — the weekly review adapts the entire program:

| Goal | Reps | Sets | Rest | Style |
|------|------|------|------|-------|
| Strength | 3-5 | 5 | 2.5 min | Compound-heavy |
| Hypertrophy | 8-12 | 3-4 | 75s | Compound + isolation |
| Weight Loss | 12-15 | 3 | 35s | Supersets, circuits |
| Mobility | 10-12 | 3 | 60s | Full ROM, lighter loads |
| General | 8-10 | 3 | 90s | Balanced mix |

## Weight Progression Rules

After each week, Claude compares your logged reps to the prescribed rep range (e.g. 8-10):

| What happened | Next week |
|---------------|-----------|
| All sets hit top of range (e.g. 10) + RPE ≤ 7 | **Go up** (+5-10 lbs barbell, +5 lbs dumbbell, +5 lbs curl bar) |
| All sets hit top of range + RPE 8+ | **Stay** — you got the reps but it was hard |
| All sets within range but not all at top | **Stay** — keep building toward the top |
| Any set below the range (even one) | **Drop 5-10%** — weight is too heavy |
| Exercise skipped / not logged | **Stay** — no change |

Dumbbells move in **5 lb increments only** (no 2.5 lb dumbbells available).

### Examples (range 10-12)

| Sets logged | Result |
|-------------|--------|
| 12, 12, 12 @ RPE 6 | Go up |
| 12, 12, 12 @ RPE 9 | Stay |
| 12, 11, 10 | Stay |
| 12, 12, 9 | Drop — 9 is below 10 |
| 10, 9, 8 | Drop — 9 and 8 are below 10 |

## Deload (Big 3 Only)

If the average RPE on bench, deadlift, and squat stays at 9+ for **3 consecutive weeks**, Claude auto-programs a deload week for those 3 lifts only:

- Weights drop to 50-60% of normal
- 1 fewer set
- Extra 30s rest
- Same exercises — stay in the groove
- All accessories stay at normal weight

After the deload, weights return to pre-deload levels.

## Exercise Library

~60 exercises tagged by muscle group, movement pattern, equipment, and goal suitability. Categories include:

- **Barbell**: bench, squat, deadlift, OHP, row, RDL, hip thrust, shrug, curl, etc.
- **Dumbbell**: presses, flyes, rows, lunges, split squats, RDLs, curls, raises, etc.
- **Cable / pulley**: lat pulldown (wide & close), straight-arm pulldown, tricep pushdown (rope & bar), overhead tricep rope, face pull, cable crunch
- **Leg attachment**: leg extensions, leg curls
- **Dip bars**: dips (chest), tricep dips, captain's chair knee raise
- **Bodyweight**: push-ups, pull-ups, chin-ups, planks, dead bugs, ab wheel, hanging leg raise
- **Curl bar (EZ bar)**: EZ bar curl

## Mobile Logger Features

- Dark theme, big tap targets, one-thumb operation
- Auto-fill weight from previous logged set (so dropping weight on set 2 carries to set 3)
- RPE picker (1-10) after each set
- Rest timer between sets
- Edit logged sets to fix mistakes
- Day picker to preview any workout day
- Progress dashboard with PR cards, big 3 trend chart, weekly volume, and quick stats
- Live plan loading from GitHub repo (no stale data)

## Project Structure

```
├── index.html                  # Mobile workout logger (hosted on GitHub Pages)
├── data/
│   ├── settings.json           # Current goal, pinned exercises, equipment, deload tracking
│   ├── exercise-library.json   # ~60 exercises with metadata
│   ├── weekly-plan.json        # This week's workout plan (fetched live by the logger)
│   ├── history.json            # Aggregate of all parsed workout logs (powers dashboard)
│   └── logs/                   # Per-day workout log JSON files
├── AUTO_SEND_SETUP.md          # Optional: auto-send daily emails via Apps Script
├── ROADMAP.md                  # Future feature ideas (~80 across 14 themes)
└── README.md
```

## Automations

| Trigger | Schedule | What it does |
|---------|----------|-------------|
| Daily Workout Email | 6 AM Mon/Wed/Fri | Creates Gmail draft with today's workout + logger link at the top |
| Workout Log Ingestion | 10 PM nightly | Parses any new "Workout Log" emails into `data/history.json` so the dashboard works across devices |
| Weekly Review | 7 PM Sunday | Reads Gmail logs, adjusts weights, rotates exercises, writes next week's plan, sends summary |

## Data Persistence

Your workout data is stored in three places (in order of permanence):

1. **Gmail** (forever) — Every "Workout Log" email is permanently in your inbox. The canonical source.
2. **`data/history.json`** in GitHub (forever, accessible from any device) — Updated nightly. The dashboard reads from here.
3. **Phone localStorage** (per-device) — Only used during the workout itself for in-progress tracking.

Switch phones, reinstall, clear cache — your data is safe.

## Links

- **Workout Logger**: https://travis-coder135.github.io/workout-planner/
- **Manage Triggers**: https://claude.ai/code/scheduled
- **Auto-Send Setup**: see [AUTO_SEND_SETUP.md](AUTO_SEND_SETUP.md) to send daily emails automatically without tapping send
- **Roadmap**: see [ROADMAP.md](ROADMAP.md) for future feature ideas
