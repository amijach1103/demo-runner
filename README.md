# A demo that drives itself

One HTML file that walks a product prototype through a scripted sequence, narrates each step in synthesized speech, and moves on only once the narration has actually finished. I built it in one day for a studio recording of an early-stage prototype at work. It isn't a library, it has no tests, and it was never turned into a product. The content is rewritten as a neutral example; the mechanism and the reasoning are the work.

| File | What it is |
|---|---|
| [`demo-runner.html`](demo-runner.html) | 14 scenes, styles and script included, no dependencies and no build step. Open it in a browser |

## The problem

The prototype had simulated AI: the responses were pre-scripted, nothing was saved, and a refresh wiped everything. It demoed well when it behaved and badly when it didn't, and it was about to be recorded in a studio for an outside audience. A live walkthrough puts three things that can go wrong on camera at once: typing, timing, and whatever the prototype decides to do that day.

So the demo stopped being something a person performs and became something the page performs. The person running it just presses play.

## What it does

- **Scenes as data.** Each scene is a name, a voiceover line, and what to show. Adding a scene means adding an entry, not rewiring the flow.
- **Narration in sync, not on a timer.** The obvious version guesses how long a line takes and sets a timer. That drifts right away, and worst on the longest sentences. This waits until the voice has finished before moving on, so the picture and the words can't separate.
- **The view follows the narration.** When the voice mentions something, the page scrolls to it, so viewers never hunt for what's being described.
- **A fixed frame.** The product sits on one side and the scene list on the other, so the recording has a steady layout to crop to.

## The part worth reusing

Move on when the speech ends, never on a timer. It's the difference between a demo that holds together and one that slowly slides out of sync while the camera is running, and it's about four lines of code.

## Running it

Open `demo-runner.html` in a browser. It uses the browser's own speech, so there's no key, no network call and nothing to install. Voices and timing differ between browsers, which is exactly why each step waits for the speech to end instead of a measured duration.

---

More of my work: [github.com/amijach1103](https://github.com/amijach1103) · MIT license
