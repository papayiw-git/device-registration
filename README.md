# FilterCycle (internal idea key: Device Registration / #2)

## Overview
FilterCycle is a mobile-first app (PWA-style prototype) that solves one problem: people forget to
change the filters in their water purifier, air conditioner, air purifier and vacuum cleaner until
the appliance breaks down or gets dirty. The app lets a homeowner register each appliance once,
tracks the change cycle automatically, and reminds them before the next change is due, with a
one-tap link to reorder the same filter model.

Category: Home & household appliances. Fidelity: hi-fi, single visual direction (navy / white
utility palette). Platform: mobile app first (390px), with a desktop companion (1440px) for the
device dashboard and settings screen only.

## Files in this handoff
- `DeviceRegistration.dc.html` — the real, working single-flow app. Every screen is wired to
  actual state (React-style component state) persisted to `localStorage`, so adding a device,
  marking a filter as changed, snoozing a reminder, exporting CSV, switching language, etc. all
  produce a real, visible result and survive a page reload.
- `DeviceRegistrationOverview.dc.html` — a static, pannable/zoomable gallery that lays out all 13
  screens/frames of the app side by side (auth, core flow, supporting screens, empty/error states,
  desktop companion) so every screen can be reviewed independently, the way you'd review artboards
  in a design file.
- `ios-frame.jsx` — shared iPhone device-frame component used by both files above (status bar,
  dynamic island, home indicator). Not an app screen itself.
- `images/device-*.png` — generated product illustrations (one per appliance type: water filter
  cartridge, air-conditioner filter, air-purifier filter, vacuum filter) used on the Add Device and
  Device Detail screens in place of a stock photo.

## How to open / run
Both `.dc.html` files are self-contained HTML documents — double-click or open either one directly
in a modern browser (Chrome, Safari, Edge). No build step, server, or install required. They read
and write `localStorage` under the `filterCycle.*` keys, so your data (devices, language choice)
persists between visits in the same browser.

## Features (working app)
- Onboarding, login and sign up (mock auth — any non-empty email/password logs in).
- Home: device list, each card shows a progress ring, status badge (on track / due soon / overdue)
  and the next-change date, plus quick totals.
- Add / edit device: name, type, brand & model (sample data, editable), install location, last
  change date, change-cycle presets (30/60/90/180 days) or a custom value, notes.
  Validates required fields with inline errors.
- Device detail: big progress ring, change history, "mark as changed today" (recalculates the next
  due date instantly), and an "order the same filter" button linking to a sample order page for
  that model.
  Includes a delete flow with an inline confirm step.
- Search & filter: free-text search plus status and appliance-type filters.
- Alerts: auto-generated reminders for devices that are due soon or overdue, each with a "view
  device" and "snooze 7 days" action.
- Settings: account, push-reminder toggle and lead time, CSV export (real file download), reset
  sample data, delete all devices (drives the empty state), and a "simulate error" switch used to
  demo the network-error state safely, without needing a real outage.
- Empty state and error state, both reachable from the running app (delete all devices / toggle
  simulate error in Settings) rather than only mocked in isolation.
- Desktop companion (1440px): a two-pane dashboard + settings layout for the device overview and
  settings screens only, toggled from the top bar.

## Language switching (EN / TH)
Every screen, validation message, empty/error/success copy and the sample data itself (device
names, locations, notes) has an English and Thai version. Toggle the "TH / EN" pill in the top bar
of `DeviceRegistration.dc.html` at any time; the choice is saved and re-applied on reload. Dates are
localized (Buddhist calendar for Thai, Gregorian for English).

## Naming rationale
The internal idea key is "Device Registration" (โจทย์ #2: ลงทะเบียนอุปกรณ์). That key describes the
input mechanic, not a product a person would remember, so the shipped UI uses the short brand name
"FilterCycle" (Thai: "รอบไส้กรอง") instead. The idea key is preserved here for traceability.

## Limitations
- Auth is intentionally mocked (no real backend, no password rules) — this is a front-end
  prototype, not a production auth system.
- Brand/model names and order links are placeholder/sample data, clearly labeled as such in the UI.
- Push notifications are represented as in-app alerts (Alerts screen); there is no real device
  push integration in this handoff.
- Only two screens (device dashboard, settings) have a dedicated desktop layout, matching the
  brief — all other screens are mobile-only by design.

## Screenshots

| Desktop dashboard | Desktop settings |
| --- | --- |
| ![FilterCycle desktop dashboard](screenshots/device-registration-desktop-dashboard.png) | ![FilterCycle desktop settings](screenshots/device-registration-desktop-settings.png) |

## Repository

https://github.com/papayiw-git/device-registration
