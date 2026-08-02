# JavaScript Drum Kit

A lightweight, browser-based drum kit built with HTML, CSS, and vanilla JavaScript. Press one of the supported keyboard keys to play its associated drum sound and display a short visual response.

## Features

- Plays nine local WAV audio samples from the keyboard.
- Allows the same sound to be triggered repeatedly without waiting for it to finish.
- Animates the corresponding drum key while its CSS transition runs.
- Requires no package manager, build step, framework, or server-side code.

## Running the Project

Clone or download the project, then open `index.html` in a modern web browser.

For the most consistent browser behavior, serve the directory with a simple local static server. For example, if Python is available:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000` in your browser.

## Keyboard Mapping

| Key | Sound |
| --- | --- |
| A | Clap |
| S | Hi-hat |
| D | Kick |
| F | Open hi-hat |
| G | Boom |
| H | Ride |
| J | Snare |
| K | Tom |
| L | Tink |

## Project Structure

```text
.
├── index.html       # Page markup, audio elements, and interaction logic
├── style.css        # Layout, visual styling, and active-key animation
├── background.png   # Full-page background image
└── sounds/          # WAV samples used by the drum kit
```

## How It Works

Each visible drum pad in `index.html` has a `data-key` value containing its keyboard key code. An `<audio>` element with the same `data-key` points to the matching sound file.

When a key is pressed, the `keydown` listener:

1. Locates the matching audio element and drum pad.
2. Resets the audio element's `currentTime` to `0`, so quick repeated presses replay immediately.
3. Starts playback and applies the `playing` CSS class to the matching pad.

The `playing` class scales the pad and adds an accent border and shadow. When the `transform` transition ends, the `transitionend` listener removes the class so the pad returns to its default appearance.

## Technologies

- HTML5
- CSS3
- JavaScript (DOM APIs and HTML Audio API)

## Customization

To change a sound, replace the relevant WAV file in `sounds/` or update the corresponding audio element's `src` attribute. To add a drum pad, add a visible `.key` element and an `<audio>` element that share the same `data-key` value, then provide the audio file.

## Browser Support

This project is intended for current versions of modern desktop browsers with JavaScript and audio playback enabled.
