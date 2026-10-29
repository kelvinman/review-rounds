---
name: Clear docs
kind: docs
---

## 01 Start with the task
Open with what the page helps the reader do, in one sentence. Concepts come after the steps, or on their own page.
- Before: The configuration system uses a layered model inherited from v1.
- After: This page shows how to change where logs are saved.

## 02 One action per step
Number the steps. Each step has one action, and its result if the reader needs to check it.
- Before: 1. Open settings, choose Storage and set the path, then restart.
- After: 1. Open Settings. 2. Choose Storage. 3. Set the path. 4. Restart the app.

## 03 Commands and values the reader can copy
Put commands, paths and values in code formatting, exactly as typed. Show placeholders as `<like-this>` and say what to put there.
- Before: Run the install command with your key.
- After: Run `tool install --key <your-api-key>`, using the key from the dashboard.

## 04 Say what's required first
List what the reader needs before they start (accounts, versions, permissions) at the top, not when they hit an error.
- Before: (step 5) If this fails, you may need admin rights.
- After: Before you start: you need admin rights on the workspace.

## 05 Second person, present tense
Address the reader as "you" and describe what happens now.
- Before: The user will then be shown a confirmation.
- After: You see a confirmation.

## 06 Define a term once, then use it the same way
Explain a term the first time it appears. Never use two names for the same thing.
- Before: Create a project. Then add files to the repo.
- After: Create a project (a folder the tool tracks). Then add files to the project.

## 07 Errors and limits stated plainly
When something can fail or has a limit, say what, when and what to do.
- Before: Large files may cause issues.
- After: Files over 100 MB fail to upload. Split them first.

## 08 Keep it current
Remove steps, screenshots and options that no longer exist. Check every step against the product before proposing it.
- Before: Click the gear icon in the top right.
- After: Open Settings from the sidebar.
