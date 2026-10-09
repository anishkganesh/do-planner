# do.

A browser-based lifestyle planner for tasks, goals, habits, and personal progress. The complete application lives in a single HTML file and stores its data locally in the browser.

## Overview

`do.` combines a task manager, goal planner, habit tracker, and dashboard without a backend or build step. It is a local-first prototype: the profile and sharing interfaces operate on records in the same browser, rather than on a hosted account service.

## Features

- Create, edit, prioritize, schedule, complete, and reorder tasks.
- Organize tasks into active and completed views.
- Record goals and a personal vision statement.
- Track habits, streaks, calendar activity, and statistics.
- Switch between guest and locally stored profiles.
- Export and import planner data as JSON.
- Use built-in quotes and local task-processing helpers.

## Architecture

`index.html` contains the markup, CSS, application state, and JavaScript event handlers. Data is serialized into `localStorage` for the current browser origin. Export/import provides a manual way to move or back up that data.

The task-processing helpers, including `simulateLLMProcessing`, use local heuristics. They do not call a language-model API. There is no server-side user database, email delivery service, or cross-device synchronization.

## Tech stack

| Layer | Implementation |
| --- | --- |
| UI | HTML, CSS, browser JavaScript |
| Persistence | Browser `localStorage` |
| Backup | JSON export/import |
| Hosting | Static hosting; `CNAME` contains custom-domain configuration |

## Project structure

- `index.html` — the complete planner.
- `CNAME` — custom-domain configuration for static hosting.

## Run locally

```bash
git clone https://github.com/anishkganesh/do..git
cd do.
python -m http.server 8000
```

Open `http://localhost:8000`. Python is only a convenient static file server; there are no application dependencies to install. Any equivalent static server can be used.

## Configuration and data

No API keys, environment variables, database, or package installation are required. Keep using the same browser origin to access the same stored planner data. A different hostname, port, browser, or device has separate storage.

Export a JSON backup before clearing browser storage. Import only backups you intend to use, and review the resulting planner state.

## Usage

Start as a guest or create a local profile, add tasks, define goals, and check off habits as you complete them. Use the dashboard to review progress and export data when you want a backup.

## Validation

No automated tests or build scripts are included. To check the planner, create and edit tasks, reorder them, record a habit, reload the page, and verify that export/import preserves the intended data.

## Deployment

Publish the root files to a static host such as GitHub Pages. A custom domain additionally needs the host and DNS configured to match `CNAME`. The repository configuration does not establish whether the domain is currently reachable.

## Limitations

- Local profile passwords are stored in browser storage in plaintext. These profiles are unsuitable for sensitive account authentication.
- The verification interface displays a code locally; it does not send verification email.
- Sharing is scoped to records in the same browser origin.
- Clearing local storage removes data unless a backup is available.

## Attribution and license

No standalone license file is included. This README does not grant a new license.
