# model-viewer

Lightweight browser-based STL and STEP viewer built on Three.js.
Drop it anywhere — GitHub Pages, a VPS, whatever and point it at a model file via URL param.

Example:  [Setup](https://viewer.mechaxil.com/?flags=upload,edit)

## Usage
```
viewer.html?file=https://raw.githubusercontent.com/you/repo/main/part.stl
viewer.html?file=https://github.com/you/repo/blob/main/part.step
```

GitHub blob URLs are rewritten to raw automatically.

## Flags
```
?file=…&flags=edit,upload
```

| Flag | What it does |
|------|-------------|
| `edit` | Scale input, Auto Orient, Confirm |
| `upload` | Local file picker (.stl / .step / .stp) |

## Formats

- **STL** — binary and ASCII
- **STEP** — via OpenCASCADE WASM (occt-import-js), loads on demand

## postMessage API

Send a model from a parent frame:
```js
iframe.contentWindow.postMessage({
  type: "load_model",
  buffer: arrayBuffer,
  ext: "step"
}, "*")
```

Confirmation comes back as:
```js
{ type: "model_confirmed", data: { rotation: [x, y, z], scale: 1 } }
```

## Self-hosting

Single HTML file, no build step. Just serve it.
