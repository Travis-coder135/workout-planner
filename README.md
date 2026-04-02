# Workout Planner

A personalized workout system powered by Claude that acts as your personal trainer. It emails you your daily workout, lets you log sets on your phone, and automatically adjusts your program each week based on your performance.

## How It Works

```
Monday/Wednesday/Friday at 6 AM
  → Gmail draft with today's workout + target weights
  → Open mobile logger on phone
  → Log weight, reps, RPE after each set
  → Tap "Email Log" when done

Sunday at 7 PM
  → Claude reviews your week's logs
  → Adjusts weights based on RPE
  → Rotates exercises for variety
  → Writes next week's plan
  → Sends you a weekly summary
```

## Setup

- **Equipment**: Home gym — barbell, power rack, full dumbbell set
- **Schedule**: 3 lifting days (Mon / Wed / Fri), runs separately on Thursdays
- **Split**: Push / Pull / Legs
- **Session**: ~45 minutes

## Pinned Exercises

These are always the first exercise on their day and never get swapped out:

| Day | Exercise |
|-----|----------|
| Monday (Push) | Barbell Bench Press |
| Wednesday (Pull) | Barbell Deadlift |
| Friday (Legs) | Barbell Back Squat |

## Goals

Change your training goal anytime — the weekly review adapts the entire program:

| Goal | Reps | Sets | Rest | Style |
|------|------|------|------|-------|
| Strength | 3-5 | 5 | 2.5 min | Compound-heavy |
| Hypertrophy | 8-12 | 3-4 | 75s | Compound + isolation |
| Weight Loss | 12-15 | 3 | 35s | Supersets, circuits |
| Mobility | 10-12 | 3 | 60s | Full ROM, lighter loads |
| General | 8-10 | 3 | 90s | Balanced mix |

## Project Structure

```
├── index.html                  # Mobile workout logger (open on phone)
├── data/
│   ├── settings.json           # Current goal, pinned exercises, preferences
│   ├── exercise-library.json   # ~50 exercises with metadata
│   ├── weekly-plan.json        # This week's workout plan
│   └── logs/                   # Parsed workout logs (per day)
├── ROADMAP.md                  # Future feature ideas
└── README.md
```

## Weight Progression Logic

After each week, Claude adjusts target weights based on your RPE (Rate of Perceived Exertion):

- **RPE ≤ 6** (felt easy) → increase weight 5-10 lbs
- **RPE 7-8** (challenging but doable) → keep same weight
- **RPE 9-10** (maxed out / missed reps) → decrease or hold

## Automations

| Trigger | Schedule | What it does |
|---------|----------|-------------|
| Daily Workout Email | 6 AM Mon/Wed/Fri | Reads plan, creates Gmail draft with today's workout |
| Weekly Review | 7 PM Sunday | Reads logs, adjusts weights, rotates exercises, writes next week |
