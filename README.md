## Pin & Gun

A phone-based race timer for club sailboat racing without a race committee.

Boats pin the ends of the start and finish lines with their phones, share the course by text message, and each phone runs its own countdown, calls its own over-early, and times its own finish. Whoever is scoring pastes everyone's result codes into the app and gets corrected times.

It's a single web page. No server, no accounts, no hardware in the water.

**Use it:** https://tonybuddha.github.io/pin-and-gun/ (once GitHub Pages is turned on)

---

## What it does

- **Lines from pins.** Any boat can pin either end of the start or finish line. Each end uses the median of all its pins, so more pins make a better line and one bad pin doesn't move it.
- **Course sharing by text.** The course (race name, start time and all pins) packs into a code you copy and text to the fleet. Merging codes combines everyone's pins.
- **Countdown horn.** Sounds at 5 minutes, 4 minutes, 1 minute and the start, with short ticks in the last 10 seconds. Also vibrates.
- **Pre-start numbers.** Distance from your bow to the line, time to the line at your current speed, and time to burn.
- **Over-early calls.** At the start signal the app checks your bow position. If you're over, it alarms and stays red until you return to the pre-start side, then times your restart.
- **Finish timing.** Detects your bow crossing the finish line in the right direction and works out the time between GPS fixes.
- **Scoring.** Paste result codes from every boat to get elapsed and corrected times, using PHRF time on distance or time on time, and copy the results as CSV for Sailwave.
- **Simulator.** Sails a fake boat around the current course on a fast clock, including an over-early start, so you can test a course before going out.

---

## Race day

### 1. Set up the course (one person, at the dock)

On the **Course** tab:

1. Enter the race name and start time.
2. Set the line ends you already know. For fixed marks, landmarks or charted positions, open **Pin options** and either type in coordinates or use **Set by bearing** (for example, "End B is 180° and 500 m from End A").
3. Tap **Copy course code** and text it to the fleet.

### 2. Set up each boat

1. Open the link. On first use, add it to your home screen.
2. On the **Course** tab, paste the course code and tap **Replace my course**.
3. Enter your boat name, PHRF rating, and **Phone to bow**: roughly how many meters forward the bow is from where your phone rides. The app times your bow, not your phone.

### 3. Pin the marks (on the water)

When a mark is dropped or you sail past a line end:

1. Get as close as you safely can.
2. Tap **Pin here** for that end and hold steady for 10 seconds while it averages GPS fixes.
3. If the mark is off to one side, use **Pin options** to say it's a few meters to port or starboard.
4. Text your updated course code. Other boats tap **Merge pins**.

Pins more than 30 m from the median show in red. They're probably mistakes, and you can delete them with ✕.

Pin within about 15 minutes of the start if you can. GPS error drifts over time, and pins taken close to the start share the same error as the boats crossing it, so the line stays accurate relative to the fleet.

### 4. Start

On the **Race** tab:

1. Tap **Arm horn & keep screen on**. Phones won't play sound until you tap something, and the screen has to stay on for GPS to keep working.
2. Tap **Start GPS**.
3. Mount the phone where you can see it and it can see the sky.

If you're over at the start signal, the screen goes red and the alarm sounds. Return to the pre-start side of the line (or its extensions) and start again. The app tells you when you've cleared.

### 5. Finish and send your result

When you cross the finish line, the app sounds and shows your elapsed time. Tap **Copy my result** and text the code to whoever is scoring.

### 6. Score

On the **Results** tab, paste all the result codes, one per line, choose the scoring method, and tap **Score**. **Copy as CSV** gives you something to paste into Sailwave or a spreadsheet.

- **Time on distance:** corrected = elapsed − PHRF × course distance (nm)
- **Time on time:** corrected = elapsed × 650 ÷ (550 + PHRF)

Course distance comes from the rhumb line between the middle of the start line and the middle of the finish line. Enter a distance to override it.

---

## Accuracy and limits

Read this before anyone files a protest based on a phone.

- **Phone GPS is good to a few meters.** At 6 knots, a few meters is about a second, so finish times are fine for club racing. Over-early calls within a few meters of the line are not reliable. We recommend sailing instructions that say the app only counts a boat over early if it's clearly over, and treat close calls as on time.
- **Heading comes from GPS.** The bow position is projected from your direction of travel, which is unreliable when you're barely moving. Near the line at the start, expect more error.
- **The screen must stay on.** It's a web page, so the browser stops GPS when the screen locks or you switch apps. Keep it in front of you, plugged in if you can.
- **Battery.** GPS with the screen on uses a fair amount. Start with a full charge or bring a battery pack.
- **No live tracking.** Each phone works alone. Results only exist once someone texts their code.
- **Everything is stored on the phone.** Nothing is sent to a server, and clearing your browser data erases your course setup.

### Sailing instructions

Since there's no committee boat, the sailing instructions should say:

- Line ends may be virtual marks, defined by coordinates in the course code.
- Start and finish times are taken from the app, with the over-early tolerance above.
- How and to whom result codes are sent, and the deadline.
- What happens if a boat's phone fails (for example, it may finish using a timestamped photo of a transit).

---

## Testing with the simulator

On the **Race** tab, pick a speed and a clean or over-early start, then tap **Run simulator**. The clock jumps to 5½ minutes before the start, and a fake boat sails the current course. Use it to check that a new course makes sense before anyone races on it.

The example course that comes preloaded (Pultneyville to Sodus Point) uses made-up coordinates. Don't race on it.

---

## Hosting

The whole app is `index.html`. To publish it with GitHub Pages:

1. In this repository, go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to "Deploy from a branch," choose `main` and `/ (root)`, and save.
3. After a minute or two the app is live at `https://tonybuddha.github.io/pin-and-gun/`.

Any change merged into `main` goes live the same way. It has to be served from a website (https); opening the file directly from your phone's downloads won't give it GPS access.

## Making changes

- Propose changes as pull requests. One person approves them, so the version the fleet uses doesn't change mid-week.
- Test every change with the simulator, then on the dock, before race day.
- Report problems as GitHub issues and say what phone and browser you're using.

The code is one file of plain HTML, CSS and JavaScript with no build step. The race logic (line crossing, over-early checks, finish timing) is in the section marked `race engine`.
