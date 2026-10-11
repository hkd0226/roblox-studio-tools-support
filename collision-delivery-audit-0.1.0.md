# Collision Delivery Audit 0.1.0 customer quickstart

This guide describes the exact Studio-tested 6a3f07ee release candidate. Native QA and GUI simulation passed; final sales readiness, upload and public availability are pending. It is not a release or purchase receipt.

## Install and first comparison

Install the Collision Delivery Audit plugin, stop Play/Run, then open Plugins > CDA. Download [CDA-Customer-Source0-0.1.0.rbxlx](CDA-Customer-Source0-0.1.0.rbxlx) and open this supplied script-free three-Part example in Studio: Workspace > CDA_3Part_Default_Example contains anchored Body, Door and Trigger, all in Default. The frozen example has SHA-256 ccda55b1c69c631c0e3f391dc40455974d33ba3913063b5954fc3e1c90c28f6b (1725 bytes). The customer example itself contains no scripts or plugin code.

1. Select the whole example Model, then click Capture selected. Wait for Current Workspace snapshot captured.
2. Click Use current snapshot as baseline. The status should show 3 recorded Parts.
3. Click Compare baseline with fresh selection. With this unchanged example, the baseline and current selected counts are both 3; required missing, other missing, pair differences and target-only groups are all 0.
4. This only compares recorded group names and pair values. It does not certify Part identity, original assignments, physics or gameplay.

## Copy and import a baseline

Click Show current snapshot JSON, click inside Output, then Ctrl+A and Ctrl+C. Click inside Portable baseline JSON, select all and paste with Ctrl+V. Click Import baseline JSON. A valid import reports Validated baseline imported; project untouched. Keep a manual copy outside the plugin if needed; no automatic file saving or persistent baseline storage is provided.

An invalid JSON or oversized UTF-8 input is rejected and retains the previous baseline. The input limit is 65,536 UTF-8 bytes, not characters. Actual GUI testing rejected 21,846 Korean characters (65,538 UTF-8 bytes) while retaining the earlier 3-Part baseline.

## Selection, cancellation and Edit mode

Select only Body. Previous output is invalidated; Show current snapshot JSON requires a fresh completed capture. Compare again: baseline 3 and current 1 are separate selected scopes. A count difference alone is not proof of missing object identity or lost assignment.

Clear / Cancel clears tool baseline and current output and cancels an active scan. The actual GUI clear operation and native cancellation checks were tested; a GUI busy-race cancellation was not separately timed. Changing selection invalidates the current result. Results are snapshots; rescan after changes.

Capture is Edit-mode only. Actual Run-mode Capture was rejected with Stop Play/Run; Edit mode only. Stop the test session normally before using the tool. A full Studio restart resets the in-memory baseline; reopen the plugin and recapture or import manually. Do not expect a baseline to survive a restart.

## Scope and limits

Workspace Models, Folders or BaseParts only. Outside Workspace, unsupported roots, WorldModels and nested WorldModel branches are rejected. Maximum 200 selected Parts, 5,000 selected-scope objects and 32 registered groups. Group names are 1-100 UTF-8 bytes without control characters. Overlapping selections are deduplicated. A rejected scan does not provide a partial successful audit.

Snapshots record all registered Workspace group names and their triangular relationship matrix, with group counts for the selected Parts. Reports distinguish baseline-used missing groups, other missing groups, pair differences among shared names and target-only groups. Target-only interactions have no source baseline.

The tool does not modify Parts/groups, restore missing assignments, register groups, repair relationships, read scripts, evaluate code, request assets or HTTP resources, or save project files. An assignment may already have become Default before a snapshot is read; the tool cannot reconstruct that earlier state. Studio Collision Groups is a capable free editor for manual changes. Paid demand and time savings are unverified.

## Support

Owner-confirmed contact addresses: hkd0226@gmail.com and hkd0226@hanmail.net. Include plugin version, selected scope and the exact error text; remove private project details from examples. No response-time promise. Buyer access, the product support link and public Roblox availability are separate checks and remain pending. This guide and the script-free example do not include the paid plugin.
