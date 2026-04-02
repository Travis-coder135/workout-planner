# Workout Planner — Roadmap

## Current System (v1)
- Mobile-first HTML workout logger with RPE tracking
- JSON-based data layer (exercise library, settings, weekly plan)
- Daily workout email (Mon/Wed/Fri at 6 AM)
- Weekly review with auto weight adjustments and exercise rotation
- Pinned exercises: Bench (Mon), Deadlift (Wed), Squat (Fri)

---

## Future Builds

### Progress Dashboard
- Visual charts showing weight progression per exercise over time
- Trend lines for pinned lifts (bench, deadlift, squat)
- Total volume per week graph
- RPE trends (are workouts getting easier or harder?)
- Personal records (PRs) tracking and highlights
- Filter by exercise, muscle group, or date range
- Could be a new tab in index.html or a separate page

### Other Ideas
- Auto-send daily email (currently creates a draft — explore Google Apps Script to auto-send)
- Google Sheets sync as a secondary database for easier data browsing
- Weekly progress photo log
- Body weight / measurement tracking
- Running log integration for Thursdays
- Rest day recovery tips or mobility routines
- Deload week auto-detection (if RPE stays high for 3+ weeks, suggest a deload)
- Exercise video/GIF links in the workout email for form reference
- Superset and circuit support in the logger UI
