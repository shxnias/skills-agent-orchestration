# Project Pulse dashboard implementation plan

## Summary

Build a small static dashboard for Mona's team that makes active projects, owners, status, recent activity, priority or risk, and concise contributor-friendly summaries easy to scan. The project brief calls for HTML, CSS, and JSON data, plus a VS Code launch configuration that serves the `app/` directory and opens `index.html`.

## Ordered implementation steps and file assignments

1. **Confirm the interface and content contract**
   - **Designer:** Define the information hierarchy, responsive layout, card structure, status and priority treatments, and accessible interaction/visual requirements. Keep the UI focused on the project information in the brief.
   - **Coder:** Confirm the data shape and how the HTML will load the JSON and stylesheet. Use a top-level `projects` array with each project containing `name`, `owner`, `status`, `recentActivity`, and `priority`.
   - **Files:** No edits required for this alignment step.

2. **Create the project data**
   - **Coder:** Create `app/project-data.json` with representative projects and the required fields. Keep values consistent with the statuses and priority labels the UI will display.
   - **Dependency:** Step 1 establishes the field names and the categories the Designer intends to present.

3. **Build the dashboard structure**
   - **Coder:** Create `app/index.html`, including the Project Pulse title, semantic page structure, and project-card rendering that loads `app/project-data.json` and references `styles.css`. Render each project's name, owner, status, recent activity, priority, and a concise contributor-friendly summary.
   - **Dependency:** Coordinate with the Designer's information hierarchy and the JSON contract from Steps 1–2.

4. **Style the dashboard**
   - **Designer:** Create `app/styles.css` for a polished, responsive dashboard with readable spacing, clear typography, project cards, status badges, and distinct priority/risk treatment. Include deterministic `.dashboard` and `.project-card` hooks and use clear contrast, rounded corners, and subtle shadows.
   - **Dependency:** The HTML structure and class names must be agreed with the Coder before styling is finalized.

5. **Make the app runnable from VS Code**
   - **Coder:** Create `.vscode/launch.json` as strict JSON, with a **Run Project Pulse Dashboard** configuration that serves from `${workspaceFolder}/app` and opens `index.html` rather than a directory listing. Use a deterministic local port and URL consistent with the chosen serving mechanism.
   - **Dependency:** The launch target depends on the static app being present at `app/index.html`.

6. **Integrate and validate**
   - **Coder:** Check the JSON and launch configuration parse, verify all referenced files and required data fields exist, and check that the page loads project data and stylesheet.
   - **Designer:** Review the rendered dashboard for information hierarchy, accessibility, responsive behavior, and visual clarity.
   - **Orchestrator:** Review the integrated app and resolve any issues reported by either specialist.

## Responsibilities and file ownership

- **Designer** owns `app/styles.css` and the visual/UX decisions: hierarchy, accessibility, responsive behavior, and consistent class hooks. Designer coordinates required markup hooks with Coder but does not edit Coder-owned files unless reassigned.
- **Coder** owns `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`; implements the data loading/rendering and runnable preview; and validates technical integration.
- **Orchestrator** sequences the work, confirms file ownership and shared contracts, delegates the steps, then reviews the integrated result.
- **Planner** defines this implementation sequence, dependencies, edge cases, and validation expectations; Planner does not implement the app.

## Dependencies and parallel work

- The data field contract and shared UI/markup hooks must be agreed before integration.
- After agreeing on the field contract and class hooks, **Designer can work on `app/styles.css` in parallel with Coder creating `app/project-data.json` and `app/index.html`**, provided both agents coordinate on the agreed hooks and do not edit each other's files.
- `.vscode/launch.json` can be prepared in parallel with styling once the app path and launch behavior are fixed, but final launch validation must wait until `app/index.html` exists.
- Integration and browser review are sequential after the app files and launch configuration are available. Any markup or class changes found in review should be coordinated to preserve the ownership split.

## Edge cases and risks

- Handle JSON loading or parsing failures visibly; do not leave an empty or success-looking dashboard if project data cannot be loaded.
- Ensure status and priority remain understandable without color alone and maintain sufficient contrast.
- Check long project names, owner names, or activity text for wrapping and overflow at narrow viewport sizes.
- Keep displayed fields aligned with the defined JSON contract so missing or inconsistent values do not break rendering.
- The exact VS Code launch mechanism and browser/debugger availability in the Codespace may vary; choose a mechanism available in the environment and ensure the resulting configuration opens the app page, not a directory listing.

## Validation expectations

- Parse `app/project-data.json` and `.vscode/launch.json` as valid JSON; ensure the launch file contains no comments.
- Confirm `app/index.html` references `styles.css` and `project-data.json`, and renders project cards with name, owner, status, recent activity, and priority.
- Confirm the data has a top-level `projects` array and each project provides `name`, `owner`, `status`, `recentActivity`, and `priority`.
- Confirm the CSS contains `.dashboard` and `.project-card`, with responsive layout, readable spacing, contrast, rounded corners, and shadows.
- Run **Run Project Pulse Dashboard** in VS Code and verify it serves from `app/` and opens `index.html`.
- Review keyboard access, semantic structure, status/priority meaning without color alone, narrow-screen layout, and behavior when project data cannot be loaded.

## Open question

- Which browser/debugger or preview mechanism is available in the target Codespace for the launch configuration? Coder should verify the available environment and choose a compatible, deterministic configuration while preserving the required launch name, `app/` working directory, and `index.html` target.
