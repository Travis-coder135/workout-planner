# Workout Planner

A personalized workout system powered by Claude that acts as your personal trainer. It emails you your daily workout, lets you log sets on your phone, and automatically adjusts your program each week based on your performance.

## How It Works

```
Monday/Wednesday/Friday at 6 AM
  → Gmail draft with today's workout + target weights
  → Tap "Open Workout Logger" link in the email
  → Log weight, reps, RPE after each set
  → Tap "Email Log" when done

Sunday at 7 PM
  → Claude reviews your week's logs from Gmail
  → Adjusts weights based on reps and RPE
  → Rotates exercises for variety
  → Writes next week's plan
  → Sends you a weekly summary with explanations
```

## Setup

- **Equipment**: Home gym — barbell, power rack, full dumbbell set, EZ curl bar, pull-up bar
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

## Project Structure

```
├── index.html                  # Mobile workout logger (hosted on GitHub Pages)
├── data/
│   ├── settings.json           # Current goal, pinned exercises, equipment, deload tracking
│   ├── exercise-library.json   # ~50 exercises with metadata
│   ├── weekly-plan.json        # This week's workout plan (fetched live by the logger)
│   └── logs/                   # Parsed workout logs (per day)
├── ROADMAP.md                  # Future feature ideas
└── README.md
```

## Automations

| Trigger | Schedule | What it does |
|---------|----------|-------------|
| Daily Workout Email | 6 AM Mon/Wed/Fri | Creates Gmail draft with today's workout + logger link |
| Workout Log Ingestion | 10 PM nightly | Parses any new "Workout Log" emails into `data/history.json` so the dashboard works across devices |
| Weekly Review | 7 PM Sunday | Reads Gmail logs, adjusts weights, rotates exercises, writes next week's plan, sends summary |

## Links

- **Workout Logger**: https://travis-coder135.github.io/workout-planner/
- **Manage Triggers**: https://claude.ai/code/scheduled
- **Auto-Send Setup**: see [AUTO_SEND_SETUP.md](AUTO_SEND_SETUP.md) to send daily emails automatically without tapping send
