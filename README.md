# mini-apps

A collection of small, self-contained web apps. Each one is a single HTML file
with no build step, no dependencies to install, and no server — open the file in
a browser and it runs.

Live at **[ivofilipe1.github.io/mini-apps](https://ivofilipe1.github.io/mini-apps/)**.

## Apps

| App | What it does | Live |
|---|---|---|
| [tide](tide/) | Paced breathing timer: cyclic breaths, an open-ended breath hold, a timed recovery hold | [open](https://ivofilipe1.github.io/mini-apps/tide/) |
| [trajectory](trajectory/) | Single-file weight and calorie tracker. Smooths the scale, fits your real energy expenditure from your own logs, and projects 90 days forward | [open](https://ivofilipe1.github.io/mini-apps/trajectory/) |

## Conventions

Every folder in this repo follows the same shape:

```
app-name/
├── index.html   the entire app
└── README.md    purpose, usage, anything worth knowing
```

`index.html` rather than a descriptive filename, so each app is served at a clean
path under Pages.

Three rules these apps hold to:

1. **One file.** No build step, no package manager, no framework.
2. **No outbound requests.** No CDN, no webfont, no analytics. Fonts come from
   the device.
3. **Namespaced storage.** Every app under `ivofilipe1.github.io` shares one
   browser origin, so anything written to `localStorage` must be prefixed with
   the app's name — otherwise one app reads another's data.

## Licence

[MIT](LICENSE) — applies to every app in this repo.
