# HeartQuake

Six bodyweight routines, each a fixed fifteen minutes: five of warm-up, ten of
work. No equipment required for five of the six.

Every exercise is compound — multiple joints, large muscle mass, and a real
heart-rate response. There is no isolation work, and there is no set or rep
counting. You work for the interval, you rest for the interval, the app tells
you what is next.

## Safety — read before using

Warm up first. The app makes you, so do not skip it by turning every warm-up
movement off. Stop if something sharp or one-sided starts hurting — muscle burn
is fine, joint pain is not. **This is a timer, not a coach: it cannot see your
form.** Get medical clearance first if you are pregnant, recovering from injury,
or have a heart condition. Nothing here is medical advice.

This warning is also shown in the app itself, above the settings.

## The routines

| Routine | Impact | Heart rate | Trains |
|---|---|---|---|
| **Ground & Up** | High | High | Legs, push, core |
| **Stretch** | None | — | Mobility |
| **Single Side** | Low | Moderate | Legs, balance |
| **Hinge & Hold** | None | Low | Back, glutes, core |
| **Bar** | Low | Moderate | Back, biceps, core |
| **Upper** | Low | Moderate | Chest, shoulders, triceps |

The impact and heart-rate labels are the point of having six routines rather
than one shuffled deck. "Evening, apartment, downstairs neighbours" is a visual
scan, not a feature you have to go looking for.

**Ground & Up** is deliberately leg-dominant. Heart rate is driven by recruited
muscle mass and the legs are where the mass is; that is *why* interval training
looks like this. Balance comes from rotating across routines over a week, not
from balancing inside one ten-minute block.

**Bar** alternates bar work and floor work on purpose. Grip and lats fail long
before cardio does, so a pure hanging circuit stops being interval training by
the third round.

**Upper** needs nothing at all, so it stands in for Bar when there is no bar.
Between them they are the only pulling in the app — bodyweight training without
equipment is otherwise all push, quad and hip flexor, and that imbalance shows
up eventually as shoulder and lower-back complaints.

## How the fifteen minutes is spent

**Warm-up** — six movements, fifty seconds each. Shared by every routine,
including Stretch.

**Work** — twelve intervals of forty seconds on, ten seconds off.

The twelve slots are fixed. If you have turned exercises off, the remaining ones
come round more often — the session never gets shorter, it gets more repetitive.
With all six enabled each one appears twice.

**Stretch is the exception.** Holds are not intervals, so the ten minutes is
divided evenly across side-slots instead: six stretches, ten side-slots, sixty
seconds each.

Exercises that work one side at a time say `Left side first` and then chime
`Switch sides` at the halfway mark, inside the same forty-second interval.

## Equipment

Everything runs with nothing at all. Each item you have swaps one exercise for a
better version of it:

| Toggle | What changes |
|---|---|
| Pull-up bar | Unlocks the Bar routine |
| Elastic band | Band row instead of Superman row |
| Stable surface | A chair, step or couch edge — dips instead of shoulder taps |
| Wall | Wall walks, and a deeper hip flexor stretch |
| Jump rope | Replaces jumping jacks in the warm-up |
| Foam roller | Rolling instead of two of the stretches |

Bar is the only routine gated behind equipment; it greys out with the reason
stated rather than offering you a workout you cannot do.

## Exercises you can't do

One toggle per exercise, on or off. **No reason is asked for and none is
stored** — injury, strength, mobility, a bad wrist, it makes no difference to
what the app does.

Groups start collapsed, so the sheet opens as seven headers rather than
thirty-nine switches. Each header carries a live count — `4 of 6 on` — so you
can see a group has something switched off without opening it.

Toggles are shared across routines: an exercise you cannot do is one you cannot
do wherever it appears, so turning off Burpee removes it from both Ground & Up
and Bar. The sheet lists each exercise once and notes where it is reused.

Thirty-nine exercises in total. If a routine drops below three available
exercises the app says so, both on the routine card and in the list, rather than
quietly serving you the same two things twelve times.

## Running it

Open `index.html` in a browser. That is all — no build, no install, no server.

Works on desktop and mobile. It requests a screen wake lock so the display does
not sleep mid-session; browsers that do not support that will simply dim as
usual.

## Controls

| Action | Input |
|---|---|
| Pause and resume | Tap anywhere on the stage, or press `Space` |
| Abandon the session | `End` button, or press `Escape` |
| Close the exercise sheet | `Done` button, or press `Escape` |

Ending early still shows the summary for what you actually did.

## The display

The stage drains left to right over the current interval, so how much of it is
left is readable from the floor without focusing on the number. Colour carries
the phase: amber for warm-up, red for work, green for rest.

Under each exercise name is a looping stick figure showing the shape of the
movement. Where a pose would otherwise be an ambiguous diagonal, it is drawn
with its scenery — the bar you hang from, the wall your feet are on, the edge
you dip from — because a hang and a plank are the same line without it.

Views are chosen per exercise rather than kept consistent. Prone Y-T-W is drawn
from above, because a side view flattens Y, T and W into the same silhouette;
Superman stays side-on, because the lift is the whole point of it.

During a work interval the figure replaces the cue text: you are moving, not
reading. The cue comes back during the ten-second rest, alongside the figure
for whatever is next — so the rest is spent preparing rather than waiting.

`prefers-reduced-motion` holds the first frame instead of looping.

## Cues

- **Sound** — a tone on every change, a double tone on `Switch sides`, and three
  ticks counting an interval out. Synthesised in the browser with oscillators;
  nothing is downloaded, so there is no delay before the first beep.
- **Vibration** — one long pulse for work, two short for rest, three for a side
  switch, so the change is distinguishable in a pocket. **Android only** — iOS
  browsers do not expose the vibration API, and the toggle disables itself when
  unsupported.

## Storage

`localStorage`, under the key `heartquake.v1`, holding four things: the routine
you last picked, which equipment you have, which exercises are off, and your
sound and vibration preferences.

**No session history is kept.** Nothing is recorded about what you did, when you
did it, or how you performed, and there are no dates in the store at all. It is
a preferences file, not a training log.

Nothing is sent anywhere. There is no account, no analytics, and no network
request of any kind — the page's Content-Security-Policy sets `connect-src
'none'`, so `fetch`, `XHR` and `sendBeacon` cannot fire even if markup were
somehow injected.

The key is namespaced because every app under `ivofilipe1.github.io` shares one
browser origin. A copy opened from your own disk keeps a separate store from the
hosted one — same app, different origin, so settings do not carry across.

## Notes and known limitations

- **The timer relies on `requestAnimationFrame`**, which browsers suspend for
  hidden pages. Switching tabs or apps mid-session pauses the count rather than
  letting it run in the background. The wake lock keeps the display awake, but
  it cannot help if you navigate away.
- **The figures show shape and nothing finer.** A stick figure has no wrists,
  no spine curvature and no shoulder rotation, so it cannot show *elbows at
  45°*, *ribs down*, *flat back* or *squeeze the shoulder blades* — which are
  the exact things a beginner gets wrong. That is what the cue text is for, and
  the two are meant to be read together. If you have not done an exercise
  before, look it up rather than trusting either one alone.
- Archer push-up and the other one-sided exercises animate a single side; the
  `Switch sides` cue owns the other half, so the figure does not mirror.
- **The heart-rate labels are descriptive, not measured.** Nothing here reads
  your pulse. They rank the routines against each other, and that is all they
  claim.
- Collapse state in the exercise sheet is not remembered; it opens all-collapsed
  every time. Deliberate — it is ephemeral UI, not a preference worth storing.

## Type

No webfonts. A serif italic (Georgia, falling back through Iowan Old Style and
Palatino to the generic serif) carries exercise names; the platform UI sans
carries numbers and controls. Instruction reads spoken, data reads neutral.

Using fonts already on the device means no third-party request, no font flash on
load, and `index.html` stays genuinely self-contained. Numerals use
`font-variant-numeric: tabular-nums` so the countdown does not shift width as it
counts.

## Licence

Code is [MIT](../LICENSE).
