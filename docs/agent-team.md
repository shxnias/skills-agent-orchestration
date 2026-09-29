# Agent team for Mona's Project Pulse dashboard

I am using the GitHub Copilot CLI in a Codespace to orchestrate the build of Mona's Project Pulse dashboard. The custom agent team is defined under `.github/agents/` and is designed to split planning, design, implementation, and coordination so the work stays organized and parallel where possible.

- Planner — model: Claude Opus 4.7 (copilot). Responsible for researching the repo, identifying dependencies and edge cases, and producing the implementation plan the team will execute. Definition: `.github/agents/planner.agent.md`.
- Designer — model: Gemini 3.1 Pro (copilot). Responsible for the UI/UX direction, information hierarchy, accessibility, and the visual styling needed for a polished Project Pulse dashboard. Definition: `.github/agents/designer.agent.md`.
- Coder — model: GPT-5.5 (copilot). Responsible for implementing the code changes, app logic, and any required runnable app support in the assigned scope. Definition: `.github/agents/coder.agent.md`.
- Orchestrator — model: Claude Opus 4.7 (copilot). Responsible for coordinating the Planner, Designer, and Coder agents, sequencing work, assigning file scopes, and validating that the integrated result works together. Definition: `.github/agents/orchestrator.agent.md`.

This team gives Mona's Project Pulse dashboard a clear workflow: the Planner scopes the work, the Designer shapes the experience, the Coder builds the implementation, and the Orchestrator keeps the project moving in a single GitHub Copilot CLI-driven Codespace environment.
