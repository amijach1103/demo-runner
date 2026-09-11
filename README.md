# A demo that drives itself

A single self-contained HTML file that walks a product prototype through a scripted
sequence, narrates each step in synthesized speech, and advances only once the narration
has actually finished.

⚠️ **Status and scope, stated first because it is the thing most easily overstated.** This
was built in one day for a single studio recording of an early-stage prototype. It is not a
library, it has no tests, and nothing here was productised. The content has been rebuilt as
a neutral example; the mechanism and the reasoning are the work.

| | |
|---|---|
| **[`demo-runner.html`](demo-runner.html)** | 14 scenes, inline styles and script, no dependencies and no build step. Open it in a browser |

---

## The problem it started from

The prototype it was made for had **simulated AI**. The responses were pre-scripted, there
was no persistence, and a refresh wiped everything. It demoed well when it behaved and badly
when it did not, and it was about to be recorded in a studio for an external audience.

A live walkthrough puts three things that can go wrong on camera at once: typing, timing,
and whatever the prototype decides to do that day.

⭐ **So the demo stopped being something a person performs and became something the page
performs.** The operator's job shrank to pressing play.

## What it actually does

- **Scene sequencing.** Each scene is a data object: a name, a voiceover line, and the
  markup to show. Adding a scene is adding an entry, not rewiring a flow.
- **Narration in sync, not on a timer.** The obvious version is to guess how long a line
  takes and set a timeout. That drifts immediately, and it drifts worst on the longest
  sentences. This waits for the speech-synthesis end event before advancing, so the picture
  and the words cannot separate no matter how the voice is rendered.
- **Auto-scroll to the subject.** The narration says a thing and the view moves to that
  thing, so the viewer is never hunting for what is being described.
- **A fixed device frame.** The product sits unobstructed on one side, the scene list on the
  other, so the recording has a stable composition to crop to.

## The part worth stealing

**Advance on speech-end, never on a timer.** It is the difference between a demo that holds
together and one that slowly slides out of sync while the camera is running, and it is about
four lines of code.

## Running it

Open `demo-runner.html` in a browser. Speech synthesis is the browser's own, so no key, no
network call, no install.

⚠️ Voices and timing differ between browsers, which is exactly why the advance is bound to
the end event rather than to a measured duration.
