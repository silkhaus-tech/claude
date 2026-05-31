# Skill: Run Ops Summary Report

## Description
Find the latest ops performance PDF in Google Drive, read it, and produce a structured summary of wins, drops, and key callouts. Trigger when asked to "run ops summary" or "summarise the QuickSight report".

---

## Steps

1. **Find the latest file strictly inside the 'Ops Report' folder in Google Drive:**
   - Use Google Drive search to locate the folder named **'Ops Report'** and get its folder ID.
   - Then search for files with `parents in '<folder_id>'` to list **only** files directly inside that folder.
   - Sort results by `modifiedTime descending` and pick the **first result** — that is the latest file.
   - Do **not** search in 'Autosaved Files', root, or anywhere else. If no files are found inside 'Ops Report', stop and tell the user no report was found in that folder.

2. **Identify the most recent completed week based on today's date:**
   - A "completed week" means the week where data is fully populated (no zero values or missing entries).
   - Do not treat the current in-progress week as the latest week even if it appears in the report.
   - Compare that week against the immediately preceding week only.
   - Label the summary with the correct week-ending date.

3. **Read through all the metrics in the PDF:**
   - For each metric note: current completed week value, previous week value, target, and whether it is above or below target.
   - Skip any week rows where data appears incomplete or shows 0 without an obvious reason.

4. **Identify the top 3 biggest drops:**
   - Worst performance vs target, or largest week-on-week decline.
   - Prioritise metrics that are furthest from target.

5. **Identify the top 3 biggest wins:**
   - Best performance vs target, or largest week-on-week improvement.
   - Prioritise metrics that have crossed back above target.

6. **Write a 3-sentence executive summary:**
   - Most urgent issue first.
   - End on the single most encouraging trend.
   - No fluff, suitable for an ops team lead.

7. **Create a Gmail draft** to `maulik@silkhaus.co` with the output below.

---

## Output Format

**Subject:** `Ops Performance Summary — Week ending [date]`

**🔴 Biggest Drops**
- [Metric name]: [value] vs target [target] — [one line on why it matters]
- [Metric name]: [value] vs target [target] — [one line on why it matters]
- [Metric name]: [value] vs target [target] — [one line on why it matters]

**🟢 Top Wins**
- [Metric name]: [value] vs target [target] — [one line on what improved]
- [Metric name]: [value] vs target [target] — [one line on what improved]
- [Metric name]: [value] vs target [target] — [one line on what improved]

**Summary**
[3 sentences max. Most urgent issue first. End on the encouraging trend.]

---

## Context

- **Company:** Silkhaus, short-term rental operator in Dubai and Abu Dhabi
- **Report source:** Amazon QuickSight, emailed weekly
- **Metrics span:** Customer Experience, Guest Coordination, LiveOps, Guest Relations, Maintenance, Cleaning
- **Targets:** Defined in the PDF itself — always compare against them
- If a metric shows 0% or no data for the current week, treat it as incomplete and skip it
- **Tone:** Direct, no fluff, suitable for an ops team lead

---

## Trigger Phrases
- "run ops summary"
- "summarise the QuickSight report"
- "ops report"
