# 🏸 Badminton Tournament Leaderboard

A single-page web app for running a badminton tournament: import fixtures from Excel, enter scores, get live standings on a TV, and generate the knockout bracket.

- No database and no server. Everything runs in the browser.
- Works offline once the page has opened. It also runs straight from a pen drive (just open `index.html`).
- Handles round robin and cross-group fixtures, and detects which one it is from the fixture sheet.

---

## 1. Put it online (GitHub Pages, one time)

1. Create a **public** repository on GitHub, e.g. `badminton-leaderboard`.
2. Upload `index.html` (and this README) to the repository.
3. Go to **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, branch **main**, folder **/ (root)**, then Save.
4. After about a minute the app is live at
   `https://<your-github-username>.github.io/badminton-leaderboard/`

Anyone with the link can use it, with no login and without you being there. Only the app code is public. Tournament data never leaves the laptop where it is entered.

**Backup plan:** copy `index.html` to a pen drive. Double-clicking it opens the same app, even without internet.

---

## 2. Before the tournament

1. Open the app and go to **Setup → Choose file**, then select the organizers' fixture Excel.
   - Any layout works. The app guesses which column is Match No / Team 1 / Team 2 / Group / Court / Time, and you can correct each one.
   - One column like `Smashers vs Hawks` also works (choose *"same cell as Team 1, split on vs"*).
   - A separate **Teams** sheet (team → group) is optional but helps catch misspelt names.
   - For an easy start, give the organizers `fixture_template.xlsx`.
2. Press **Check fixtures**. The app shows:
   - **Detected format:** Round robin / Cross group (and the pairs, e.g. A + B)
   - Warnings for missing or duplicate matches, misspelt teams, or a team playing itself
3. Press **Start tournament**.
4. In the **Setup** tab (cross group only), choose how standings are shown:
   - One combined table per pair (A + B), or
   - Each group separately (A, B)
5. In the **Knockout** tab, choose:
   - **Next round:** Round of 32 / 16 / Quarter-finals…
   - **Selection:** *Top N per table + best next-placed teams*, or *Overall ranking*
   - **Pairing:** *High vs low seed* (1 v 32) or *Cross-group* (table winners v lower places of the next table)
   - Deuce and third-place match on/off

   Qualifying teams appear **gold** in Standings and on the TV as the league progresses.

## 3. On the day

1. Connect the laptop to the TV and set the display to **Extend**.
2. Press **📺 Open TV display**, drag the new window to the TV, and double-click it for full screen.
3. Keep the main window on the laptop. In **Matches**, tap a match, type both scores, and press **Enter**. The TV updates instantly.
   - **Walkover (not played):** choose *Walkover* and the winner. It is recorded 0–0; the winner gets the win and points, and point difference is unchanged.
   - **Retired mid-game (injury):** choose *Retired*, enter the score at that moment (e.g. 10–8) and the winner. The score counts toward point difference.
   - Wrong score? Tap the match again to edit or clear it.
4. **Every few matches:** go to **Backup & Settings → Download backup**.
5. When the league is finished:
   - Check **Standings** for ⚠ ties. If two teams are level on everything, decide (e.g. coin toss) and press **↑** on the winner.
   - Go to **Knockout → Generate knockout bracket**, then tap each knockout match to enter its score. Winners move on automatically.
6. At the end: **Backup & Settings → Results to Excel** gives the organizers a full report.

## 4. Rules used

| | |
|---|---|
| League game | One game, first to 21, no deuce |
| Knockout game | First to 21, deuce on/off (win by 2, max 30) |
| Points | 2 per win (changeable) |
| Table ranking | Points → Point difference → Points scored → Head-to-head (if they played) → Organizer's order |
| Best next-placed teams across tables | Points → Point difference → Points scored |
| Knockout seeds (table-based selection) | Table winners first, then 2nd places, etc.; same place ranked by points → PD → points scored |
| First knockout round | Teams from the same table never meet (opponents are swapped automatically) |

Scoring numbers, deuce, third-place match and the TV mode (auto-rotate / standings / bracket) can all be changed in **Backup & Settings**.

## 5. Important

- **Use one laptop and one browser for the whole day.** Data is saved in that browser.
- **Don't use an Incognito/Private window.** It forgets everything when closed.
- **To move to another laptop:** download a backup, open the app there, then use **Restore backup**.

---

### For developers
`index.html` is built from `src/` (engine, UI, CSS) with the SheetJS library inlined:

```
python3 build.py        # writes dist/index.html
node test/engine.test.js
```
