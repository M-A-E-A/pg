# Accessible Interactive Photo Gallery

A single-file, accessible photo gallery built with HTML, CSS, and vanilla JavaScript. It supports both mouse and keyboard interaction and is designed to pass W3C, WAVE, and aXe validation.

## Features

- **Six images** with descriptive `alt` text
- **Mouse interaction** — hovering a figure highlights it (`mouseover` / `mouseleave`)
- **Keyboard interaction** — each figure is focusable via `tabindex="0"` and highlights on focus (`focus` / `blur`)
- **Auto tabindex assignment** — a `for` loop adds `tabindex` to every `figure` on page load
- **Console logging** — every event handler logs a message to help verify triggers in DevTools
- **Accessible markup** — proper heading hierarchy, `<title>` in the head, and alt text on all images

## Project Structure

```
photo-gallery/
├── index.html   # The entire gallery (HTML + CSS + JS in one file)
└── README.md
```

## How It Works

| Function | Trigger | Purpose |
|---|---|---|
| `addTabFocus()` | Page load (`DOMContentLoaded`) | Loops through all figures and sets `tabindex="0"` |
| `showCaption(fig)` | `mouseover` | Highlights the figure border |
| `hideCaption(fig)` | `mouseleave` | Removes the highlight |
| `focusFigure(fig)` | `focus` | Highlights the figure border for keyboard users |
| `blurFigure(fig)` | `blur` | Removes the highlight when focus leaves |

Each figure is wrapped in an IIFE inside the loop so every listener is bound to the correct element (avoids the classic `var` closure bug).

## Setup

1. Download or clone the repository.
2. Open `index.html` in any modern browser — no build step or server required.
3. Open DevTools (F12) and watch the Console while you hover and tab through the images.

## Testing

### Mouse
Hover over each image. A blue border should appear, and the console should log `onmouseover event triggered`. Moving away logs `onmouseleave`.

### Keyboard
Press `Tab` repeatedly. Focus should move through each figure in order, applying the blue border, and log `onfocus event triggered`. Tabbing away logs `onblur`. The page load itself logs `addTabFocus triggered`.

### Validators
- **W3C Markup Validation Service** — https://validator.w3.org/
- **WAVE** — https://wave.webaim.org/ (or the browser extension)
- **aXe** — aXe DevTools browser extension

All three should report no errors. If you swap in your own images, remember to keep the `alt` attributes and don't skip heading levels.

## Customizing

- **Change images**: Replace the `src` URLs in each `<figure>` and update the matching `alt` text and `<figcaption>`.
- **Change colors**: Edit the `#1a5fb4` values in the `<style>` block.
- **Add more images**: Copy an entire `<figure>` block. The loop and tabindex logic handle any number of figures automatically.

## Hosting

Because it's a single static file, you can host it for free on:
- **GitHub Pages** — push to a repo, enable Pages in Settings
- **Netlify** — drag and drop the folder at https://app.netlify.com/drop
- **Your school server** — upload via FTP/SFTP

## Known Pitfalls (from peer review)

- Missing `tabindex` blocks all keyboard access
- Calling `querySelectorAll` before the DOM loads returns an empty list
- Using `var i` directly in loop handlers binds every listener to the last figure
- Missing `alt` text or a skipped heading level fails Wave/W3

## License

Free to use and adapt for coursework.
