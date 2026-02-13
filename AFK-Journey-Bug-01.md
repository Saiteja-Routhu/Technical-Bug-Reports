QA Case Study: UI Race Condition in AFK Journey

Target App: AFK Journey (Mobile)
Category: UI/UX & Functional Logic
Status: Documented for Portfolio

1. Executive Summary

During exploratory testing of the "Town Overview" systems, I identified a race condition in the building upgrade drawer. The UI lacks input debouncing, allowing rapid taps to trigger both "Open" and "Dismiss" logic simultaneously. This results in a high-frequency flicker and prevents user progression.

2. Environment

Device: [Samsung S23 Ultra]

OS: [Android 16]

Game Version: Latest Public Build (as of Feb 12, 2026)

3. Steps to Reproduce

Navigate to the Town/Overview section in the top-right.

Open the Buildings tab.

Rapidly double-tap any building icon located in the upper half of the screen.

Observe the UI drawer's behavior.

4. Observed Result

The drawer initiates an "Open" animation and immediately triggers a "Close" animation. This happens so fast that the upgrade menu is inaccessible, and the screen flickers violently.

5. Expected Result

The system should implement Input Debouncing. After the first tap is registered, subsequent taps should be ignored until the drawer transition animation is complete or the UI state is "Locked."

6. Technical Root Cause Analysis

This is a classic UI State Race Condition.

The Trigger: The building icons are located in the "Dismissal Zone" (the area of the screen that normally closes the drawer).

The Bug: Because there is no cooldown (debouncing) on the input listener, the second tap in the rapid sequence is registered by the background's "click-to-close" logic before the drawer has finished opening.

7. Visual Evidence

[https://drive.google.com/file/d/1LhxvkGO-m3f-m6VpAPmqpHQjzSv1PADa/view?usp=sharing]
