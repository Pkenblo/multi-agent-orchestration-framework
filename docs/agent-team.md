# Agent Team for Project Pulse Dashboard

## Overview

This project uses a coordinated team of four custom agents, orchestrated through GitHub Copilot CLI in a Codespace. Each agent brings specialized expertise to plan, design, and build Mona's Project Pulse dashboard—a lightweight static dashboard for displaying project information, ownership, status, and activity.

## The Agent Team

### 1. Orchestrator
- **Model**: Claude Opus 4.7 (copilot)
- **Location**: `.github/agents/orchestrator.agent.md`
- **Responsibility**: Coordinates all work by breaking down complex requests into phases and delegating to specialist agents. Does not implement code itself. Manages dependencies, handles file ownership, runs work in parallel when safe, and validates the final integrated result.
- **Key Skills**: Planning workflow, dependency management, delegation, validation
- **Entry Point**: This is the primary agent learners interact with through the GitHub Copilot CLI

### 2. Planner
- **Model**: Claude Opus 4.7 (copilot)
- **Location**: `.github/agents/planner.agent.md`
- **Responsibility**: Creates implementation strategies before any code is written. Researches the codebase, dependencies, edge cases, and implicit requirements. Produces a practical plan with ordered implementation steps, file assignments, dependencies, parallel work opportunities, edge cases, and validation expectations.
- **Key Skills**: Codebase research, documentation review, risk identification, strategic planning
- **Workflow**: Responds to Orchestrator requests; does not stage, commit, or push changes

### 3. Designer
- **Model**: Gemini 3.1 Pro (copilot)
- **Location**: `.github/agents/designer.agent.md`
- **Responsibility**: Handles UI/UX, accessibility, information hierarchy, interaction flow, and visual design. For Project Pulse, creates a polished dashboard with project cards, status badges, responsive layout, readable spacing, rounded corners, shadows, and clear typography. Ensures deterministic CSS hooks (`.dashboard`, `.project-card`) for consistency.
- **Key Skills**: Visual design, user experience, accessibility, responsive layout, design documentation
- **Workflow**: Works within assigned file scope (primarily `app/styles.css`); does not commit changes

### 4. Coder
- **Model**: GPT-5.5 (copilot)
- **Location**: `.github/agents/coder.agent.md`
- **Responsibility**: Implements code and logic within assigned file scope. Creates support configuration files such as `.vscode/launch.json`. Follows predictable project layout and existing patterns. Validates changes before reporting completion.
- **Key Skills**: HTML/CSS/JSON coding, configuration, file creation, validation
- **Workflow**: Works on assigned files only (e.g., `app/index.html`, `app/project-data.json`, `.vscode/launch.json`); does not stage, commit, or push changes

## Coordination Model

The **Orchestrator** is the primary entry point:
1. Receives requests from the learner
2. Consults the **Planner** to research and strategy before implementation
3. Delegates **Design** work to the Designer (CSS, visual direction)
4. Delegates **Implementation** work to the Coder (HTML, JSON, configuration)
5. Manages parallel vs. sequential execution based on file scope overlaps and dependencies
6. Validates the final result and provides a handoff summary

**Key Principle**: The learner controls all git operations through Copilot CLI. No agent stages, commits, or pushes code.

## Technology Stack & Environment

- **Primary Interface**: GitHub Copilot CLI in VS Code (Codespace)
- **Static Stack**: HTML, CSS, JSON (no frameworks or build tools required)
- **Configuration**: `.vscode/launch.json` for running the dashboard locally
- **Data Format**: `app/project-data.json` with a top-level `projects` array
- **Preview**: Launch configuration serves the app directory and opens `index.html` in the browser

## Project Pulse Deliverables

The agent team will coordinate creation of:
- `docs/project-pulse-plan.md` — Planner's implementation strategy with phases and file ownership
- `app/index.html` — Dashboard markup (Coder)
- `app/styles.css` — Polished dashboard styling with deterministic hooks (Designer)
- `app/project-data.json` — Project data with name, owner, status, recentActivity, priority (Coder)
- `.vscode/launch.json` — Launch configuration for previewing the dashboard (Coder)
- `docs/final-handoff.md` — Orchestrator's validation and completion summary
