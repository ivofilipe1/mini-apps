# Wandeling

A Dutch practice app built around one idea: you learn a language by using it, not
by reviewing it.

It is a walk through a town. Ninety stops, ninety fixed everyday conversations. At
each one somebody says something to you in Dutch and you answer. Words you pick up
come back a few stops later as spaced-repetition practice, and you can rehearse
what you will say before you say it. The people in the scenes are the people you
tell the app about, and the scenes use their names from then on.

Built for one learner going from A2 to C1. The scenes are scripted, not generated:
the fixed conversations are the product.

## Licence — source-available, not open source

**Wandeling is not MIT, unlike the other apps in this repo.** It is under the
[PolyForm Noncommercial License 1.0.0](LICENSE): you may use, run, change and share
it for noncommercial purposes — personal use, study, teaching, research, a charity.
Commercial use is not granted.

That makes it *source-available*, not open source: the Open Source Definition does
not allow a licence to exclude a field of use. Some organisations' policies bar
such code outright. The licence requires every copy to carry its terms, which is
why this folder has its own `LICENSE` and the licence line is also printed in the
app's footer.

Two third-party works are inside the file and keep their own terms. See
[Credits](#credits).

## Running it

Open `index.html` in a browser. No install, no account, no server, and it works
offline.

Use the same browser every time: progress lives in that browser, on that device.
Before you move the file, switch browser or device, or replace it with a newer
build, use **Settings → Backup & storage → Download backup**, then **Restore** in
the new copy.

A copy opened from disk keeps a separate store from the hosted one — same app,
different origin, so progress does not carry across without a backup. Some browsers
(Firefox especially) lose a file's progress if the file is moved or renamed.

The Dutch is read aloud by your device's own speech voice. If it sounds wrong, add
a Dutch voice in your device's language or speech settings.

## Storage

`localStorage`, under the single key **`wandeling.v4`**. It holds your word list,
spaced-repetition state, notes, how far you have walked, the names you gave the
cast, and your preferences.

The app writes a short-lived test key, `wandeling.__probe`, to check that storage
works, and removes it straight away. Nothing else is written.

The names and details you give the cast can describe real people. They stay in your
browser and are included in any backup you download, so treat a backup file as
personal data. Backups never contain model settings or an API key.

**Reset all data** in Settings clears the key and says what it is about to delete.

## Optional AI features

Free-form conversation, goals, custom scenes and bulk meaning fill need a language
model. They are off by default and the app never uses a model to grade your Dutch.

**They are switched off on this shared site.** Every app under
`ivofilipe1.github.io` shares one browser origin, and an API key saved here would
sit in storage that the other apps on that origin can read. So on any host other
than a file on your own computer or `localhost`, the provider, key and endpoint
settings are greyed out and the features stay off — whatever is already in storage.

To use them, save `index.html` and open it from disk (or serve it from `localhost`),
then paste your own key from Claude, OpenAI or Gemini under **Settings → Model**.
The key stays in your browser and goes only to the provider you pick; use a key with
a spend limit. This is the only outbound request the app can make, and only after
you switch it on.

With the features off, the app makes no network requests.

## How this copy is made

This is a **generated file**, not hand-written source, so unlike the other apps it
has a build step, just not in this repo. The source lives in a separate repository
([ivofilipe1/Wandeling-app](https://github.com/ivofilipe1/Wandeling-app), which is
not necessarily public). Its build script splices the scenes, the sentence data and
the font into one HTML file.

The copy committed here was built from commit `d799e09` on 2026-10-12. Settings →
diagnostics in the app shows the same stamp (`d799e09, 2026-10-12`). The stamp never
ends in `+edits`: that suffix means the build came from a tree with uncommitted
changes, and such a build is not published here.

**To update this copy:**

1. In the source repo, commit your change, then run `python3 src/build.py --release`.
2. Confirm the stamp has no `+edits`.
3. Replace `wandeling/index.html` here with the new `index.html`, and check the copy
   is byte-identical.
4. Update the commit and date above, and commit. One commit per release, not per build.

Keep the storage key `wandeling.v4` stable across updates, so people's progress
survives. If a change breaks the saved data's shape, bump the key and write a
migration rather than reusing it.

## Size

About 1.2 MB, roughly 390 KB over the wire when Pages serves it compressed. It is
larger than the other apps because the ninety scenes, the word pool, the example
sentences and a 66 KB font are all inside the file.

## Credits

- **Example sentences** are from [Tatoeba](https://tatoeba.org), used under
  [CC BY 2.0 FR](https://creativecommons.org/licenses/by/2.0/fr/) and credited to
  the Tatoeba Project and its contributors. They are not covered by the PolyForm
  licence and keep their own terms, which permit commercial use. The app credits them
  in its footer.
- **Fraunces** is the serif that carries the Dutch text. It is by Phaedra Charles
  and Flavia Zimbardi, under the [SIL Open Font License 1.1](OFL.txt). It is embedded
  in the page as a base64 `@font-face`, so no font is requested over the network.
  Because the OFL requires each copy to carry its licence text, the full text is in
  [`OFL.txt`](OFL.txt) in this folder.

## Notes and known limitations

- **Speech depends on the device.** The voice is whatever the browser exposes; there
  is no bundled audio. A device with no Dutch voice falls back to its default.
- **Progress is per browser, per origin.** Clearing site data, or private browsing,
  loses it. Download a backup first.
