# Tide

A paced breathing timer for cyclic breathing with breath retention.

One round is three phases:

1. **Paced breaths** — a set number of breaths at a fixed cadence.
2. **Hold, empty** — after the last exhale, an open-ended hold. Untimed; you end
   it yourself when you need air. The app records how long it lasted.
3. **Hold, full** — one big breath in, held for 15 seconds.

Repeat for as many rounds as you set.

## Safety — read before using

Fast cyclic breathing lowers blood CO₂ and **can make you faint with no
warning**. Sit or lie down before you start. Never do it in or near water, in a
bath, while driving, or standing up. Stop if you feel unwell. Get medical
clearance first if you are pregnant, or have epilepsy, high blood pressure, or a
heart condition.

This warning is also shown in the app itself, above the settings.

## Attribution and disclaimers

Inspired by the cyclic breathing pattern popularised by the Wim Hof Method. This
project is not affiliated with, endorsed by, or connected to Innerfire BV or Wim
Hof, and nothing here is medical advice — it is a timer, not a health
intervention, and it has not been reviewed by anyone with medical
qualifications. The underlying technique of cyclic hyperventilation followed by
apnea long predates any modern branding of it. Consult a doctor before starting
any breathing practice.

## Running it

Open `index.html` in a browser. That is all — no build, no install, no server.

Works on desktop and mobile. It requests a screen wake lock so the display does
not sleep mid-session; browsers that do not support that will simply dim as usual.

## The display

The whole screen area is the vessel, and it reads as your lungs: it **fills from
the bottom** as you inhale and **drains** as you exhale. Empty during the
empty-lung hold, full during the recovery hold. The phase is legible from across
the room without reading the numbers.

## Controls

| Action | Input |
|---|---|
| End the empty-lung hold | Tap anywhere on the stage, or press `Space` |
| Abandon the session | `Stop` button, or press `Escape` |

Ending the session early still shows the summary, as long as you completed at
least one hold.

## Settings

**Pace** — three presets as starting points (Slow, Steady, Brisk), or type the
inhale and exhale durations in milliseconds directly. Inhale accepts
600–8000 ms, exhale 400–8000 ms. The cycle length updates as you type.

**Shape** — 1 to 10 rounds, and 20 to 60 breaths per round in steps of 5. The
duration estimate assumes 75-second holds, purely so the number is not blank; it
is not a target or a recommendation.

**Cues** — three independent toggles:

- *Breath sounds* — synthesised rising and falling air. Nothing is downloaded;
  it is brown noise through a sweeping bandpass filter, generated in the browser.
- *Hold chime* — marks the start and end of each hold.
- *Vibration* — one pulse in, two out, three on a phase change, so the phase is
  distinguishable without looking. Sub-toggles let you keep phase-change buzzes
  while dropping the per-breath ones. **Android only** — iOS browsers do not
  expose the vibration API, and the toggles disable themselves when unsupported.

## Summary

At the end: every hold as a bar scaled against your longest, plus the longest
hold and total session time.

## Notes and known limitations

- **Nothing is stored and nothing is fetched.** No `localStorage`, no cookies,
  no analytics, and no network requests of any kind — the page makes zero
  outbound connections. Settings reset on reload and hold times are gone when you
  close the tab. Deliberate, but it means there is no history.
- **`prefers-reduced-motion` is currently ineffective.** The rule disables a CSS
  transition, but the tide is animated by per-frame transforms, so reduced-motion
  users still get the full animation. Needs a real fix.
- The pace preset stays visually selected after you hand-edit the millisecond
  fields, even though the values no longer match the preset.

- **The timer relies on `requestAnimationFrame`**, which browsers suspend for
  hidden pages. Switching tabs or apps mid-session pauses the count rather than
  letting it run in the background. The screen wake lock keeps the display awake,
  but it cannot help if you navigate away.

## Type

No webfonts. A serif italic (Georgia, falling back through Iowan Old Style and
Palatino to the generic serif) carries the spoken-language cues; the platform UI
sans carries numbers and controls. Data reads neutral, instruction reads spoken.

Using fonts already on the device means no third-party request, no font flash on
load, and `index.html` stays genuinely self-contained. The design depends on the
contrast between the two voices, not on one specific typeface. Numerals use
`font-variant-numeric: tabular-nums` so the timer digits do not shift width as
they count.

## Licence

Code is [MIT](../LICENSE).
