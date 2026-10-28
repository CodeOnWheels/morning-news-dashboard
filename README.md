# Morning News Dashboard

A standalone, responsive morning briefing designed to be refreshed by a ChatGPT scheduled task. ChatGPT researches the news and rewrites the HTML; the browser displays the saved edition.

The shared HTML uses placeholders for local coverage and the poll. Fill them during your first local refresh.

The five sections are **Local News**, **World News**, **Stock Market**, **Tech News**, and **Sports**. Local coverage focuses on [YOUR CITY / REGION]; sports covers national college football.

## How the scheduled refresh works

1. A local ChatGPT Work/Codex task starts at **[REFRESH TIME] [YOUR TIMEZONE]**.
2. It reads the existing dashboard, researches a complete fresh edition, and verifies the sources and dated data.
3. It writes and validates a temporary HTML file before replacing the dashboard.
4. It reports success or failure. If research or validation fails, it keeps the last complete edition.

The HTML contains no scheduler, live feed, or API integration. Downloading this repository does not create a ChatGPT task. A run starting at the configured time may take several minutes to finish.

**Current status:** the included page is the manually prepared October 19, 2026 historical test edition, “Shifting Ground.” No successful scheduled refresh has been confirmed. Its intended information cutoff is [REFRESH TIME] [YOUR TIMEZONE]; market data and the AP poll have their own dates. The reporting has not received a complete independent article-by-article audit.

## Limitations

- **Static snapshot:** the browser displays the saved edition. It does not fetch live news, prices, or rankings; reloading the page does not research a new edition.
- **Automation is not yet demonstrated:** no successful scheduled refresh has been confirmed. The repository includes refresh instructions, but no executable refresh pipeline, scheduler, or API integration.
- **Validation depends on the task:** source checks, backups, and safe file replacement are requirements in the refresh prompt, not guarantees enforced by repository code. No automated test suite or continuous integration is included.
- **Reporting needs review:** AI-generated summaries can contain factual errors, unsupported claims, incorrect dates, or broken citations. The historical test edition has not received a complete independent article-by-article audit. Check the original sources before relying on its reporting or market figures.
- **The sample is incomplete:** local coverage and the AP Top 25 use placeholders. Personalize the setup and complete a verified refresh before treating the dashboard as a finished briefing.
- **Local setup is required:** refreshes depend on a compatible ChatGPT environment, web and file access, account availability, and the local computer being available. A configured schedule does not prove that a run completed; inspect the run history and output.
- **Reliability is unmeasured:** repeated scheduled runs, recovery from failures, factual accuracy, and cross-browser accessibility have not been documented through a reproducible evaluation.
- **External resources can change:** source pages may move, become unavailable, or require a subscription. Favicons are loaded from Google's service, so opening the page sends third-party image requests.

## Open the dashboard

Download or clone this repository, then open `index.html` in your browser. Bookmark that file and keep its location stable. All HTML, CSS, and theme JavaScript are contained in this one file; no build step is required.

The dashboard defaults to dark mode and saves your light/dark preference locally. Article links and Google's favicon service need an internet connection.

## Set up a daily ChatGPT task

### 1. Give the task access to your dashboard

Use ChatGPT's desktop app with a **local Work or Codex task** that can read and write your project folder and research the web. Open the downloaded or cloned project folder and verify that the task can read `index.html`.

Use the local environment for a local bookmark. A cloud chat does not automatically gain access to a file on your computer just because its path appears in a prompt. Availability and controls depend on your account and app version.

Choose the full path of the file you want refreshed. For a new setup, this is your downloaded or cloned `index.html`. If you already have a bookmarked `morning-brief.html`, use that existing file as the target instead. Do not move or rename it.

### 2. Personalize the placeholders

Replace `[YOUR CITY / REGION]`, `[FAVORITE TEAM]`, `[REFRESH TIME]`, `[YOUR TIMEZONE]`, and `[DASHBOARD_HTML_PATH]` with your choices before using the prompt. Use an IANA timezone name for `[YOUR TIMEZONE]`. Choose no favorite team if you do not want a highlighted row. Keep personal settings in your local copy rather than committing them to the shared repository.

### 3. Test the refresh instructions once

Copy the prompt below into the local task after filling in the placeholders. Ask for one manual run before scheduling it, and inspect the resulting file in your browser.

A successful manual run proves the workflow can update the file; it does not prove a schedule is enabled.

### 4. Schedule the tested workflow

In that local task, ask:

> Schedule this dashboard refresh every day at [REFRESH TIME] [YOUR TIMEZONE], using the refresh instructions below and this local project. Keep the same dashboard file path. Return completion or failure details after each run.

Include the completed refresh prompt below with that request. Review the saved task in **Scheduled** (or the automation controls offered by your Codex app), checking its target project, instructions, enabled state, and next run. Confirm **[YOUR TIMEZONE]**, rather than a fixed UTC offset, so the intended local time follows daylight saving changes.

If using a standalone local project task, choose local project execution when the goal is to replace your bookmarked file. An isolated worktree edits a separate checkout.

For this local workflow, keep your computer awake, online, signed in, and the desktop app running at the scheduled time. Enable task notifications if desired. Do not rely on the schedule until a scheduled run has actually completed and the file has changed.

### Refresh prompt

```text
Refresh the morning news dashboard at:
[DASHBOARD_HTML_PATH]

Read the current HTML first. Research and generate one complete fresh edition
using information available by [REFRESH TIME] [YOUR TIMEZONE] on the edition date.
If execution is delayed, retain that cutoff and report the delay.

Preserve the existing design, CSS, navigation, responsive behavior, theme
buttons, locally saved theme preference, and exact destination file path.
Keep these exact section names and order:
1. Local News
2. World News
3. Stock Market
4. Tech News
5. Sports

Cover [YOUR CITY / REGION] in Local News. Cover national
college football in Sports without favoring [FAVORITE TEAM] editorially.
Do not add Politics or other sections.

Refresh the whole edition together: all five news sections, the centered
single-line 1–3 word title, edition number, date, moon phase, sourced quote,
market figures, and full latest AP Top 25 table. Determine the correct
edition number from the existing edition; do not advance it more than once
for the same edition date. Verify the moon phase for [YOUR CITY / REGION] on that date.

Use motivating, non-cliched quotes from historical figures, philosophers,
or comparable notable people, with a verifiable source and attribution.

Write concise but informative paragraphs with concrete events, names,
figures, context, and implications. Use at least three distinct source
organizations in each section; syndicated copies of the same reporting
count once. Verify article content, publication dates, figures, and links.
Do not treat search excerpts as independently confirmed reporting.
Distinguish confirmed facts, attributed claims, forecasts, and interpretation.

Keep each source on its own line with a favicon and clickable link.
Preserve the restrained paragraph layout and subtle section rules.

For S&P 500, Nasdaq Composite, and Dow Jones, show the index level, point
change, percentage change, source, and explicit actual as-of timestamp.
Use the latest completed trading session available at the cutoff. Preserve
its real session date over weekends and holidays. Never invent same-day
closing figures or relabel old figures as current.

Include the complete latest published AP college football Top 25 with its
actual publication date, all ranks and records, and tied ranks if present.
Highlight [FAVORITE TEAM]'s row only if ranked; never insert an unranked team.
If no newer poll is available, retain the latest verified poll with its
actual date rather than implying it was newly published.

Write a temporary UTF-8 HTML file in the destination folder. Validate the
five sections and their order, source organization counts, three complete
market displays and timestamps, full poll table and ties, title and date
consistency, source links, and theme JavaScript. Inspect the rendered page
when browser tools are available; report if visual inspection is unavailable.

Only after validation succeeds, preserve a backup of the last complete
edition and replace the destination safely. If research, verification,
writing, or validation fails, leave the destination unchanged and report
the failure. Never advance the displayed date while retaining old reporting.

Report the edition date, information cutoff, actual market session date,
poll publication date, destination, and validation outcome. Distinguish
a manual run from a scheduled execution.

This prompt updates the local dashboard only. Do not publish or push
changes to GitHub.
```

## Sharing the project

GitHub distributes the dashboard and these setup instructions. The dashboard runs locally on each person's computer; it does not require GitHub Pages or other hosting.

Download the repository using **Code → Download ZIP** and extract it to a permanent folder, or clone it with Git. Open and bookmark the local `index.html`, then configure your own local scheduled task using the instructions above.

Each person uses their own ChatGPT account, local file path, and schedule. Downloading or cloning the project does not copy the maintainer's task or enable updates. Scheduled refreshes change the local HTML file; they do not push changes back to GitHub.

## Check runs and troubleshoot

- **No fresh edition:** check that the task exists, is enabled, targets the correct local project and file, and has completed a scheduled run. Check for pending approvals, unavailable tools, or usage limits.
- **Computer was asleep or offline:** inspect the run history; do not assume the file refreshed or that a missed run was replayed.
- **Old date remains after an error:** this is intentional. The workflow preserves the last complete edition.
- **Browser still shows the previous edition:** reload the page and confirm the bookmark points to the same local HTML file the task updated.
- **Task produces text but does not edit the file:** confirm it is running in an environment with access to the local project, rather than an ordinary chat without local file tools.

You can edit or pause the task from its scheduling controls. Creating a task, seeing an enabled state, and observing a successful scheduled execution are separate milestones.

## Documentation

Setup guidance checked October 28, 2026. App controls and availability can change.

- [OpenAI: Scheduled tasks](https://learn.chatgpt.com/docs/automations)
- [OpenAI Help: Scheduled tasks in ChatGPT](https://help.openai.com/en/articles/10291617-scheduled-tasks-in-chatgpt)

Historical generation scripts and local backups are intentionally excluded from the shared project.
