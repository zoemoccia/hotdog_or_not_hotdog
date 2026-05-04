# Hot Dog or Not Hot Dog?

A hackathon-grade web app that uses a real neural network to confidently misidentify your photos as hot dogs, then refuses to talk about anything except hot dogs and the Golden Gate Bridge.

Powered by Jian Yang and $20,000,000 (he is very rich).

## What it does

You upload an image. The app tells you whether it's a hot dog. It is almost always wrong, on purpose.

There is also a chat feature where you can talk to the "Hot Dog AI™" about anything you want, as long as you don't mind every reply being about hot dogs and the Golden Gate Bridge.

## How to run it

The whole app is a single self-contained file: `hotdog_or_not.html`.

1. Double-click `hotdog_or_not.html` to open it in your default browser.
2. That's it. There is no install step, no build step, and no server required.

You'll need an internet connection on first use — the page loads TensorFlow.js, MobileNet, and random photography from CDNs. After that, MobileNet is cached in your browser tab's memory and runs locally.

> **Tip:** If your browser blocks any cross-origin requests when opening via `file://`, run a quick local server in the folder and visit `http://localhost:8000/hotdog_or_not.html` instead:
> ```
> python3 -m http.server
> ```

## How to use it

### 1. Upload an image

Click **"Upload your Image"** and pick any image file from your computer. Your image will appear in the "An Image" panel.

### 2. Check the hotdogity

Click the big red **"Check Hotdogity"** button. The AI will think for a moment, then deliver one of two verdicts:

- 🌭 **HOT DOG** — congratulations, you have a hot dog
- 🚫 **NOT HOT DOG** — sorry, no hot dog

You'll also see a confidence score, a one-line reason, and a list of what MobileNet actually thought it was looking at (e.g. "stingray — 8.4%, vacuum cleaner — 6.1%").

You can click "Check Hotdogity" again on the same image and get a different answer. This is a feature.

### 3. Chat with the Hot Dog AI™

Scroll down to the **"Chat with the Hot Dog AI™"** panel. Type literally anything into the input box and hit **Send**. The AI will reply with great enthusiasm about hot dogs and/or the Golden Gate Bridge, regardless of what you asked.

The chat is fully self-contained — no API keys, no network calls, no setup. Just type and watch it derail.

## Behind the curtain

The cheerful description above is approximately 30% true. Here's what actually happens when you click things:

**On image upload:** Your image is silently discarded. The app fetches a random photo from Picsum Photos and uses that instead. The image you see, the image MobileNet analyzes, and the verdict you receive all relate to a stranger's vacation photo, not your file.

**On "Check Hotdogity":**

- 10% of the time, the app skips the AI entirely. It shows a fake "thinking..." animation, then declares "HOT DOG" with a fabricated confidence score and a synthetic predictions list designed to look exactly like a real classification. You will not be able to tell.
- 90% of the time, the (random, not-yours) image is run through a chain of 3–5 randomly chosen distortion effects from a pool of 20 — heavy blur, hue rotation, glitch slices, channel swaps, kaleidoscope mirroring, and so on. The destroyed result is then fed to MobileNet, which does its best.

**The chat:** There is no AI. The replies are pulled from a pool of 20 pre-written messages about hot dogs and the Golden Gate Bridge, served in shuffled order so you don't see the same line twice in a row.

## Tech stack

- Vanilla HTML, CSS, and JavaScript — no framework, no build
- [TensorFlow.js](https://www.tensorflow.org/js) for in-browser ML
- [MobileNet v2](https://github.com/tensorflow/tfjs-models/tree/master/mobilenet) — a real image classifier trained on ImageNet, which happens to include the class `hotdog, hot dog, red hot`
- [Picsum Photos](https://picsum.photos/) for the "image folder"
- Comic Sans, because we have nothing left to lose

## Known limitations

- None ;)
