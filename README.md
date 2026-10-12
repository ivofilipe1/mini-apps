# mini-apps

A collection of small, self-contained web apps. Each one is a single HTML file
with no dependencies to install and no server — open the file in a browser and it
runs.

Live at **[ivofilipe1.github.io/mini-apps](https://ivofilipe1.github.io/mini-apps/)**.

## Apps

| App | What it does | Live |
|---|---|---|
| [tide](tide/) | Paced breathing timer: cyclic breaths, an open-ended breath hold, a timed recovery hold | [open](https://ivofilipe1.github.io/mini-apps/tide/) |
| [trajectory](trajectory/) | Single-file weight and calorie tracker. Smooths the scale, fits your real energy expenditure from your own logs, and projects 90 days forward | [open](https://ivofilipe1.github.io/mini-apps/trajectory/) |
| [heartquake](heartquake/) | Six fixed 15-minute bodyweight routines — 5 min warm-up, 10 min work. Compound exercises only, no equipment needed, remembers what you can't do | [open](https://ivofilipe1.github.io/mini-apps/heartquake/) |
| [wandeling](wandeling/) | Dutch practice by conversation: ninety fixed everyday scenes, spaced repetition and rehearsal, with the Dutch read aloud by your device's voice. Source-available, not MIT | pending |

## Conventions

Every folder in this repo follows the same shape:

```
app-name/
├── index.html   the entire app
└── README.md    purpose, usage, anything worth knowing
```

`index.html` rather than a descriptive filename, so each app is served at a clean
path under Pages. An app may carry extra files it is required to ship, such as its
own `LICENSE`.

Three rules these apps hold to:

1. **One file.** Whatever a browser needs arrives in a single HTML file. Where that
   file is generated from a source repo, its README says so.
2. **Nothing fetched behind your back.** No CDN, no analytics, no webfont request.
   Fonts are either the device's own or embedded in the file. An app may make a
   request only when you have switched it on and know where it goes.
3. **Namespaced storage.** Every app under `ivofilipe1.github.io` shares one
   browser origin, so anything written to `localStorage` must be prefixed with
   the app's name — otherwise one app reads another's data.

## Licence

[MIT](LICENSE) — applies to every app except where a folder carries its own LICENSE.
