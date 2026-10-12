# Ritme

Dutch grammar practice for a phone. Each topic starts with a short rule card, then
you practise it in quick mixed runs of twelve cards. A card you miss comes back a few
cards later in the same run and again in your next run. A card you get right comes
back after 1, 3, 7 and then 14 days, and a miss sends it back to the start.

It is the grammar companion to [wandeling](../wandeling/). Wandeling teaches Dutch
through conversation and only mentions a rule after you get a line wrong. Ritme
puts the rule first and then gives you volume: word order, verb forms, separable
verbs, de/het, connectors and a few feelings words, drilled until they come without
thinking.

## What's in it

Thirteen topics in three groups, 880 cards in total.

| Group | Topics |
|---|---|
| Word order | verb second, verb last, verb clusters, pronoun order, conjunctions |
| Verbs | perfect tense, modal verbs, separable verbs, simple past |
| Words and sound | feelings vocabulary, connected speech, connectors, de/het |

Each of the ten lessons has 52 cards: pick the right sentence, spot the mistake,
build the sentence, fill in the blank, translate, and two match-the-pairs boards.
Conjunctions has 60. De/het and simple past are drills: 150 cards each, a sample of
a larger pool of 500.

**Cards that read the sentence aloud.** The Dutch is read by your device's own
speech voice. The connected-speech topic uses it for listening: you hear a casual,
reduced form (`hebbie`, `'t is mooi`) and pick what was written. The text stays
hidden until you answer, or until you ask for it.

**Word chips or typing.** In the word-order topics you build the sentence by
tapping word chips into place, because those topics are about position and typing on
a phone is slow. A few extra words are mixed in as distractors. "Type it instead"
switches a card to typing, and Progress → Settings changes the default. Other topics
are typed, because chips would give the verb form away. Typed answers ignore case,
punctuation and accents, and say when you are one letter off.

## Running it

Open `index.html` in a browser. No install, no account, no server, and it works
offline. Use the same browser every time: progress lives in that browser, on that
device. Before you switch browser or device, use **Progress → Download backup**, then
**Restore** in the new copy.

## Storage

`localStorage`, under the single key **`ritme.v1`**. It holds, per card, which box it
is in, when it is due, and how often you got it right, plus one setting (chips on or
off) and a count of finished runs. Nothing else is written, and nothing you type is
kept. A backup file contains the same data and nothing personal.

**Reset all data** in Progress clears the key and asks first.

## Network

None. The page declares a content security policy that blocks every request, and the
app has no code that makes one. The font is the device's own.

## How this copy is made

This is a **generated file**. The lessons it comes from are kept outside this repo as
HTML pages, and a small script turns them into the one JSON blob inlined in
`index.html`. The script drops each lesson's personal framing and keeps the rule, the
examples and the exercises.

Because there is no source here, edit the generated file only for small fixes, and
regenerate from the lessons for anything bigger.

## Size

About 390 KB, of which roughly 350 KB is the card data.

## Licence and credits

The app is [MIT](../LICENSE) like the rest of this repo, with one exception.

**The 150 de/het cards are CC BY-SA 4.0.** Their gender tags and English glosses come
from [Wiktionary](https://en.wiktionary.org) through the [kaikki.org](https://kaikki.org)
extract, and the nouns were chosen using the
[FrequencyWords](https://github.com/hermitdave/FrequencyWords) Dutch list, which is
derived from OpenSubtitles. Both are licensed
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). Changes made: 150
nouns selected from a larger list, and an example sentence added to each. Those 150
cards are shared under the same licence. The app's code and everything else are
MIT.

The simple-past verb forms were cross-checked against published conjugation tables
(TaalBoost, Elon.io, coLanguage) and the 't kofschip spelling rule. The example
sentences were written for the app. The tables themselves are not copied here.

## Notes and known limitations

- **Speech depends on the device.** The voice is whatever the browser exposes. A
  device with no Dutch voice falls back to its default, and the listening cards offer
  the text instead.
- **Progress is per browser, per origin.** Clearing site data, or private browsing,
  loses it. Download a backup first.
- **A match board counts as right with one wrong tap at most**, so a single slip does
  not send the whole board back.
- **Drills are samples.** Only 150 of the 500 de/het and 500 simple-past cards ship so
  far.
