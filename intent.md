# Intent: Core Focus Timer Application

## 1. Context & Motivation
Users often struggle with distractions and burnout during long work sessions. This feature introduces a core Focus Timer based on the Pomodoro technique to help users sustain deep work, build consistency, and take structured breaks. This is the foundational feature of our productivity suite.

## 2. Requirements & Scope
Build a web-based, minimal, and highly accessible countdown timer with the following core functional requirements:

### Timer States & Durations
* Focus Session: 25 minutes (Default).
* Short Break: 5 minutes (Default).
* Long Break: 15 minutes (Default).
* Cycle: A standard loop consists of: Focus -> Short Break -> Focus -> Short Break -> Focus -> Short Break -> Focus -> Long Break (4 focus sessions total before a long break).

### Controls & Core UX
* Playback: Provide simple "Start", "Pause", and "Reset" buttons.
* Visual Cue: Show a prominent countdown clock (MM:SS).
* Tab Notification: Dynamically update the browser tab title with the remaining time (e.g., "(24:15) Focus Timer") so users can track time while in other tabs.
* Audio Alerts: Play a distinct, clean notification sound when any timer hits 00:00.
* State Switch: Automatically transition to the next logical state when a timer finishes, but require the user to manually click "Start" to begin the next session.

### Component Architecture
* Create a clean, isolated frontend component (/components/Timer).
* Manage timer state using a local state machine to prevent timer drift when the tab is backgrounded.

## 3. Out of Scope & Constraints
To prevent scope creep, the AI agent must not build the following in this iteration:
* No Persistent Storage: Do not use LocalStorage, databases, or authentication. Refreshing the page resetting the timer is acceptable for V1.
* No Custom Durations: Users cannot edit the 25/5/15 minute settings in this version.
* No Analytics/History: Do not build charts, daily streaks, or session logging.
* No Heavy Animations: Keep the UI strictly functional and lightweight. Avoid complex canvas animations for the countdown ring.

## 4. Verification & Testing Criteria
The implementation is successful if it meets the following criteria:
* Accuracy: The timer updates exactly every 1 second and handles browser tab throttling gracefully (use standard performance.now() or web workers if drifting occurs).
* UI States: The "Start" button changes to "Pause" while running. The "Reset" button restores the current session type back to its original duration.
* Audio Test: The alert audio plays reliably across modern browsers (Chrome/Safari) without breaking due to autoplay policies (ensure it only fires as a direct result of the session finishing after a user-initiated start).
* Unit Tests: Provide basic test coverage for the time-formatting utility function (e.g., converting seconds to MM:SS).
