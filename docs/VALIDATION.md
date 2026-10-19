# HoriPet verification record

This record is updated as checks are actually completed. Build success, automated application checks and native device acceptance are separate layers.

## Automated logic

42 Vitest checks cover bounded settings and corrupt inputs, offline time progression, mutually exclusive behavior priorities, drag interruption, waking, autonomous naps, cursor-follow exit, work-area clamping with negative/missing monitors, scale-independent hit regions, atomic persistence, backup recovery, immediate quit flush and the optional offline AI contract.

TypeScript checking and the production Electron/Vite build are executed before packaging. Exact results and platform-specific desktop reports are recorded with delivery evidence.

## Desktop automation

`scripts/desktop-smoke.mjs` launches a real Electron app with an isolated local profile. It checks first visible render, native transparent window color, alpha pixels, focusability, sandbox, click/double-click transitions, care actions, input rejection, hide/show/recovery, preferences and immediate settings, settings-close lifetime, offline operation, process termination and persistence across a real restart.

Playwright-delivered mouse events exercise the live renderer and IPC. They **do not alone establish native OS mouse delivery, native drag movement or transparent-region click-through**. Those require separate OS input checks. Captured PNG alpha proves the rendered surface, not every external compositor or graphics driver.

## Platform acceptance boundaries

- macOS Apple Silicon: local native application checks and installer verification are performed during delivery; the evidence report specifies completed checks.
- macOS Intel: Actions builds on an Intel runner and launches the packaged app if that job succeeds. This does not constitute manual Intel hardware/multi-monitor acceptance.
- Windows x64: Actions builds on Windows and launches the packaged app if that job succeeds. Windows 10 and Windows 11 physical desktop acceptance remains separate.
- Windows ARM64: cross-build from Windows x64; native ARM hardware execution is not claimed.
- Multi-monitor negative coordinates and DPI calculations have logic coverage. Physical monitor hot-plugging, mixed-DPI transitions, macOS Space changes and login-after-reboot must be checked on matching hardware.
- Signature/notarization, store distribution and end-user security prompts are not passed or bypassed by CI.

## Manual acceptance procedure

1. Install from the downloaded artifact, start offline, confirm the cat and a native tray icon.
2. Look behind every corner of the small pet window: no opaque rectangle, frame or shadow. Click an ordinary app through a transparent corner; that app must receive its click. Click the cat and verify the previous app keeps keyboard focus.
3. Drag the cat, including to a second monitor, release and observe a smooth state recovery. Verify right-click menu and nearby cursor follow. Move/stop the cursor and observe autonomous recovery.
4. Change language, themes, size, speed, name, skin, topmost, show/hide, sound and pause. Close preferences: the cat must remain alive. Recover from the tray.
5. Disconnect a monitor, change resolution/scaling and re-open the app with a previously out-of-range saved position. The cat must remain recoverable inside a work area.
6. Enable login startup from an installed copy, sign out and back in; disable it and verify no subsequent auto-start. Only the user enables this integration during acceptance.
7. Quit normally and inspect the process tree. Restart and verify the latest saved values. Confirm no app HTTP requests are needed.

Record the OS, CPU architecture, scaling, displays, exact artifact SHA256 and evidence for every claimed pass. Leave unexecuted items marked unverified.
