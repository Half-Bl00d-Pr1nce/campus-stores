# Campus Stores

Campus Stores is a Product Engineer work sample set at a fictional campus media equipment desk. Work through a club’s screening, from equipment pickup to a partial return and the next morning’s handover. Open **Candidate brief** in the app for the assignment.

## Run the app

Open `index.html` in a modern browser. The app includes its scripts, styles, and icons and can run offline.

To serve it over local HTTP, run this from the repository folder and visit `http://localhost:8000`.

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Each browser stores its own sample shift locally when browser storage is available. **Restart sample shift** restores the fictional starting records.

## Source

- `index.html` contains the desk layout, candidate brief, and bundled icons.
- `app.js` contains the sample records and interactions.
- `styles.css` defines the desktop and mobile layouts.

Icon license notices are in [third-party/lucide-LICENSE.txt](third-party/lucide-LICENSE.txt).

## Design & Field Notes (Candidate Submission)

### 1. One Moment That Already Works
- **Issue-slip validation checks:** When issuing equipment at pickup, the desk already validates item availability and blocks conflicting or unavailable gear from being assigned onto an open slip. That guard prevents double-booking during a rush without adding unnecessary friction, so those checks were kept completely intact.

### 2. One High-Friction Moment Changed & Why
- **What changed (`app.js`, `styles.css`):** Replaced the row-level **Record return** button in the Loan register with an auto-focused **Unit on the counter** tag check-in box.
- **Why it mattered:** In the original workflow, clicking **Record return** closed whichever open slip row was clicked without verifying the physical asset tag sitting on the counter. When two identical adapters (`AD-12` and `AD-15`) share the same bin, clicking the wrong row closes the wrong borrower's slip while leaving the actual returned unit marked out—silently desyncing the register from the shelf.
- **How the prototype works:**
  - Opening the Loan register focuses the **Unit on the counter** input immediately; typing the physical tag (e.g., `AD-12`) and pressing `Enter` closes that specific unit's active loan.
  - A **confirmation card** displays kit completeness (how many items from the booking are back vs. still out), the slip number, borrower name, due time, and a quick prompt to log a **Desk book** note if needed.
  - If an operator enters an unknown tag, a unit already on the shelf, or a unit marked in repair, a **red alert card** blocks the return, confirms nothing was closed, and names the open slip currently holding that equipment type so the operator can spot the mix-up immediately.

### 3. Film Society Shift Walkthrough (Before vs. After)
- **Before:** During the Film Society's post-screening partial return, a student drops an adapter on the desk while another club's identical adapter is also checked out. Under counter pressure, clicking **Record return** on the wrong register row closes the wrong slip with no warning, and the operator has to manually scan the table to figure out which pieces of the Film Society's kit are still outstanding.
- **After:** The operator opens the Loan register with the cursor already inside **Unit on the counter**, reads the sticker on the physical unit (`AD-12`), types it, and presses `Enter`. Only `AD-12`'s loan closes. The summary card immediately confirms that `AD-12` is checked in while listing the remaining unreturned items on the Film Society's slip along with the borrower's name, due time, and a Desk book note prompt. If a tag from another club's open loan or an already-shelved unit is entered by mistake, the red alert card stops the mismatch before any slip state changes.

### 4. One Real-Counter Observation to Measure Impact
- **Metric:** **End-of-shift shelf vs. register discrepancy count** (how often the physical count of identical-bin items like adapters/cables on the shelves disagrees with open slips in the Loan register at closing handover). A drop toward zero discrepancies at shift close—without slowing down queue clearance—confirms that tag-verified check-in eliminated wrong-row return closures.

## Submit your work

1. [Fork Campus Stores](https://github.com/virinchi-healthcare/campus-stores/fork) into your GitHub account. Complete the candidate brief and push your changes to your public fork. In your README, point reviewers to your work and explain the decision you made.
2. In your fork, open **Commits**, select the final commit you want reviewed, and copy the page URL. It should look like `https://github.com/YOUR-USERNAME/campus-stores/commit/COMMIT-SHA`.
3. [Submit your work through the Google Form](https://docs.google.com/forms/d/e/1FAIpQLScvzoh1R4WS-SkiwAVBQbMvniieJYSoOEfLMyVo5CyjOvYUgQ/viewform). Your **roll number**, **email ID**, and **final commit link from your public fork** are required. Enter your roll number and email ID in the form only.