# Auto-Send Setup (one-time, ~2 minutes)

The daily workout email is currently created as a **Gmail draft**. You can auto-send it using a small Google Apps Script that runs in your account every few minutes and sends any matching draft.

## Steps

### 1. Open Google Apps Script
Go to **https://script.google.com** (signed in as travisreynolds135@gmail.com) and click **"New project"**.

### 2. Paste this code

Delete whatever's there and paste:

```javascript
function sendWorkoutDrafts() {
  const drafts = GmailApp.getDrafts();
  drafts.forEach(draft => {
    const subject = draft.getMessage().getSubject() || '';
    if (subject.startsWith('Workout: ')) {
      draft.send();
      console.log('Sent: ' + subject);
    }
  });
}
```

### 3. Save the project
- Click the floppy disk icon (or Ctrl+S)
- Name it something like "Workout Auto-Send"

### 4. Test it once (grant permissions)
- Click the **Run** button (▶ play icon at the top)
- A popup will ask for permissions — click **Review permissions**
- Pick your Google account
- It will say **"Google hasn't verified this app"** — click **Advanced** → **Go to Workout Auto-Send (unsafe)**
- Click **Allow**

This is safe because *you wrote the script* — Google's just warning you because it's not from a verified developer. The script only sends drafts whose subject starts with "Workout: " — nothing else.

If you have a workout draft sitting in your Gmail right now, it'll send when you click Run. Otherwise it just exits silently.

### 5. Set it to run automatically
- In the left sidebar, click the **clock icon** (Triggers)
- Click **+ Add Trigger** (bottom right)
- Configure:
  - **Function**: `sendWorkoutDrafts`
  - **Event source**: Time-driven
  - **Type**: Minutes timer
  - **Interval**: Every 10 minutes
- Click **Save**

Done. From now on:

1. At 6 AM Mon/Wed/Fri, your daily workout email becomes a draft
2. Within 10 minutes, the Apps Script picks it up and sends it
3. You see it in your inbox by 6:10 AM at the latest

## How to disable
Open the Apps Script project, click the clock icon, click the trash icon next to the trigger.

## Why not run it less often (e.g. only on workout mornings)?
You could — set the trigger to "Day timer" running Mon/Wed/Fri at 6 AM. But the every-10-minutes approach is more resilient: if for any reason the trigger fires before the draft is created, the next run picks it up.

## Security note
This Apps Script only runs in your Google account, only sends drafts whose subject starts with "Workout: ", and never accesses anything else. Nothing leaves your Google account.
