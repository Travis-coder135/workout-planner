# Workout Planner — Roadmap

## Current System
- Mobile-first HTML workout logger with RPE tracking, hosted on GitHub Pages
- JSON-based data layer (exercise library, settings, weekly plan, history)
- ~60-exercise library with barbell, dumbbell, curl bar, cable/pulley, lat bar, rope, leg attachment, dip bars, and bodyweight movements
- Daily workout email at 6 AM Mon/Wed/Fri with the "Open Workout Logger" button at the top
- Nightly log ingestion (10 PM) — parses Workout Log emails into `data/history.json` so the dashboard works on any device
- Weekly review (Sunday 7 PM) with auto weight adjustments based on rep range + RPE
- Pinned exercises: Bench (Mon), Deadlift (Wed), Squat (Fri)
- Deload auto-detection for the big 3 (3 weeks of high RPE → deload)
- Day picker for previewing any workout day
- Live plan loading from GitHub repo (no stale data)
- Editable logged sets to fix mistakes
- Auto-fill weight from previous logged set (cascades through subsequent sets)
- **Progress dashboard tab** with PR cards (heaviest set + estimated 1RM), Big 3 progression line chart, weekly volume bar chart, and quick stats
- Auto-send setup guide for the daily email via Google Apps Script

---

## Future Builds (organized by theme)

### Progress & Analytics
- **RPE trends** — average RPE per week to spot when things are getting harder/easier
- **Strength standards comparison** — show how your big 3 compare to typical lifters at your bodyweight
- **Workout streak counter** — consecutive weeks hitting all 3 sessions
- **Heatmap calendar** — GitHub-style activity heatmap showing workout consistency
- **Year-in-review** — annual summary with biggest wins and total volume moved
- **Month-over-month comparison** — quick stats vs previous month
- **PR celebrations** — animated highlight when you hit a new PR

### Body Metrics & Health
- **Bodyweight tracker** — daily/weekly entries with trend graph
- **Body measurements** — chest, arms, waist, thighs, etc. over time
- **Progress photo log** — weekly photos for visual progress comparison
- **Body fat percentage** — tracked alongside bodyweight
- **Sleep tracking** — log hours and quality, correlate with workout RPE
- **Daily energy rating** — quick 1-5 score on workout days
- **DOMS (soreness) tracking** — rate soreness per muscle group for recovery insights
- **Recovery score** — combine sleep, soreness, RPE into a single readiness number

### Smart Coaching
- **AI form check** — upload a set video, get form feedback via vision model
- **Plateau detection** — flag exercises where weight has been stuck for 4+ weeks
- **Volume periodization** — auto-cycle volume across weeks (build → peak → deload)
- **Goal-specific accessory recommendations** — different accessories for strength vs hypertrophy phases
- **Chat with AI coach** — ask questions like "Should I add more back work?"
- **Event-driven plan generation** — "I have a wedding in 12 weeks, focus on aesthetics"
- **Vacation mode** — bodyweight-only plans for travel weeks
- **Hotel gym mode** — adapt workouts to limited equipment

### Workout Customization
- **Drag-to-reorder** exercises mid-workout
- **Add exercise on the fly** — quick-add a movement not in today's plan
- **Skip with reason** — log why you skipped an exercise (injury, time, equipment)
- **Substitute exercise** — swap out an exercise for an alternative
- **Custom exercises** — add your own exercises to the library
- **Multiple templates per day type** — alternate Push A and Push B routines
- **Tempo prescription** — display tempo cues like "3-1-1-0" (eccentric-pause-concentric-pause)
- **Drop sets** — log progressive weight drops within a set
- **AMRAP sets** — log "as many reps as possible" finishers
- **Time-based exercises** — for planks, holds, isometrics
- **Cluster sets / rest-pause** — advanced set structures

### UI / UX
- **Voice logging** — say "180 by 8 RPE 7" instead of typing
- **Plate calculator** — show what plates to load for a target weight
- **Haptic feedback** — phone buzz on set completion and timer end
- **PWA install** — "Add to Home Screen" prompt with proper icon
- **Offline-first** — service worker for full offline functionality
- **Set logging animation** — satisfying confirmation when a set is logged
- **Auto-advance to next set** — focus moves automatically after logging
- **Larger font mode** — accessibility option for older users or harsh gym lighting
- **Landscape optimization** — better layout when phone is sideways
- **Light mode option** — toggle for users who prefer it

### Form & Technique
- **Exercise demo videos** — embedded YouTube/GIF previews for each exercise
- **Form cues panel** — key technique reminders shown while logging
- **Common mistakes** — listed under each exercise for quick reference
- **First-time tutorial** — guided form walkthrough when an exercise is new

### Cardio & Mobility
- **Running log for Thursdays** — separate cardio tracker integrated with the system
- **Mobility routines** — daily 5-min stretches, especially on rest days
- **Warmup library** — different warmup protocols per body part
- **Cooldown stretches** — auto-suggested based on the day's exercises
- **Cardio sessions** — log incline walks, runs, intervals

### Notifications & Reminders
- **Pre-workout reminder** — push notification 1 hour before scheduled time
- **Forgot-to-log nudge** — if no log received by 8pm on a workout day
- **Hydration reminders** — during long sessions
- **Rest day mobility prompt** — gentle nudge to do mobility on off days
- **Weekly review reminder** — Sunday evening prompt to send any unsent logs
- **Push notifications via PWA** — without needing email at all

### Recovery & Wellness
- **HRV (heart rate variability) tracking** — readiness signal
- **Foam rolling guides** — targeted by yesterday's workout
- **Active recovery suggestions** — light activities for in-between days
- **Stretch routines** — by muscle group worked
- **Sleep correlation** — show how your sleep affects your RPE

### Integrations
- **Apple Health sync** — workout duration and calories
- **Google Fit sync** — same as above for Android
- **Strava integration** — auto-log Thursday runs
- **MyFitnessPal sync** — pull calorie/macro data
- **Smart scale** — auto-pull bodyweight from Withings/Eufy
- **Wearable heart rate** — during-workout HR tracking
- **Google Calendar** — auto-create workout events

### Data & Export
- **CSV export** — download all logs for analysis in Excel
- **Printable weekly plan** — paper backup for the gym
- **Backup to Google Drive** — automatic JSON backups
- **Share workout link** — send a single workout to a friend
- **Import from other apps** — Strong, Hevy, FitNotes, etc.
- **Google Sheets sync** — secondary database for easy browsing

### Habits & Lifestyle
- **Macro tracking** — protein/carbs/fat goals based on training day
- **Water intake** — daily ounces with reminders
- **Step counter** — daily activity outside the gym
- **Daily check-in** — mood, energy, motivation rating
- **Habit streaks** — gamified consistency tracking

### Voice & Hands-Free
- **Voice commands** — "next set", "skip", "log 185 8 7"
- **Read-aloud workout** — audio walkthrough at the start of session
- **Audio rest timer** — voice countdown on the last 5 seconds
- **Music integration** — start a Spotify playlist when workout begins

### Programming Templates
- **5/3/1 template** — Jim Wendler's classic strength program
- **Westside conjugate** — max effort + dynamic effort split
- **Linear progression** — Starting Strength / Stronglifts style
- **Hypertrophy specialization** — focus blocks (e.g., "arms specialization")
- **Powerlifting meet prep** — peaking protocol with timeline
- **PHAT, PPL, Upper/Lower** — multiple split options to swap between

### Email Improvements
- **Email customization** — pick what info to include
- **Multiple recipients** — send to coach/trainer in addition to yourself
- **Rich previous-week context** — "Last bench: 185x10 RPE 7, today: 190"

### Equipment Features
- **Plate inventory** — what plates you actually own (so calculator only shows realistic loads)
- **Power rack height memory** — save your J-cup positions for bench, squat, etc.
- **Equipment availability filter** — "only show what I have access to"
- **Bar weight settings** — distinguish 45 lb Olympic vs 35 lb women's vs other bars

### Variety & Engagement
- **Random workout generator** — for when you want a one-off
- **Challenge of the week** — fun mini-challenge (max push-ups, max rep test, etc.)
- **Skill progressions** — work toward muscle-ups, pistol squats, etc.
- **Bodyweight progressions** — push-up → diamond → archer → one-arm

### Social & Accountability
- **Share progress** — send a snapshot to a coach or friend
- **Coach view** — read-only access for someone helping you
- **Workout buddy mode** — log next to a partner in the same session
- **Group challenges** — opt-in shared goals with friends

---

## Recently Completed
- ✅ Progress Dashboard tab with charts
- ✅ Pinned-lift trend lines (Big 3 chart)
- ✅ Volume tracking (weekly volume bar chart)
- ✅ Personal Records (PR cards)
- ✅ One-rep max estimator (Epley formula)
- ✅ Auto-send daily email (Apps Script guide in AUTO_SEND_SETUP.md)
- ✅ Auto-fill weight from previous logged set
- ✅ Cable / leg attachment / dip bar exercises added to library
- ✅ Cross-device data persistence via nightly log ingestion
- ✅ Editable logged sets to fix mistakes
- ✅ Day picker to preview any workout day
- ✅ Logger button at top of daily email
