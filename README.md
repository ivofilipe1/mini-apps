# mini-apps

A collection of small, self-contained web apps. Each one is a single HTML file
with no build step, no dependencies to install, and no server — open the file in
a browser and it runs.

Each app lives in its own folder with its own README explaining what it is and
how to use it.

## Apps

| App | What it does |
|---|---|
| [tide](tide/) | Paced breathing timer: cyclic breaths, an open-ended breath hold, a timed recovery hold |

## Conventions

Every folder in this repo follows the same shape:

```
app-name/
├── index.html   the entire app
└── README.md    purpose, usage, anything worth knowing
```

`index.html` rather than a descriptive filename, so each app can be served at a
clean path if this is ever published.

## Licence

[MIT](LICENSE).
