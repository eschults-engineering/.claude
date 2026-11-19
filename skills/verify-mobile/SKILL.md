---
name: verify-mobile
description: Smoke test a change in a mobile app repo (an ios/ or android/ app, often with a worker/ backend) end to end before committing: run the suites it touches, then see it working in the app. Use before every commit in those repos, and when asked to verify, check or test a change there.
---

# Verify a mobile app change

Prove the change in the working tree works, the way someone using the app would see it. This skill is for repos with an `ios/` or `android/` app; in any other repo, stop and use that repo's own verify skill.

## Scope

List the changed files with `git diff --name-only main...` and `git status --short`, and check each app folder they touch: `worker/`, `ios/`, `android/`. Take the test commands from the repo's `CLAUDE.md` (its Commands section); the ones below are the fallback when it has none.

## Worker

`cd worker && npm test`

## iOS

When `xcodebuild` is missing (a cloud session on Linux), commit and push the `claude/**` branch: the iOS workflow runs the suite on the self-hosted Mac runner. Follow that run and read its failed step's log with whatever GitHub access the session has (CI notifications, a GitHub MCP, or `gh`). If no runner picks the job up within a minute, the Mac is asleep or its `runner` user is logged out: say so and stop. A cloud session cannot see the app, so report the states a local session should check.

On a Mac:

1. Run the repo's iOS test command, e.g. `cd ios && xcodebuild -quiet -scheme <App> -destination 'platform=iOS Simulator,name=iPhone 18 Pro' test`.
2. When the repo has a `screenshot` skill, run it on the states the change affects, in English and French: one moment where the change shows, and one edge case.

To rerun one Swift Testing test, name it with its parentheses, `'-only-testing:<App>Tests/<Suite>/<test>()'`: without them nothing runs and xcodebuild still prints `TEST SUCCEEDED`. Trust a single-test run only when the output names the test.

## Android

`cd android && ./gradlew test`. It needs a JDK 17 or newer: when `java` is not found, point `JAVA_HOME` at one installed on the machine.

When Gradle cannot download its dependencies (cloud sandboxes block Google's Maven), no CI runs Android yet, so say the Android change is unverified and name what a session that can build should run and check.

## Report

One line per check: what ran, and whether it passed. Fix a failure before committing, and never report a check as passed that did not run.
