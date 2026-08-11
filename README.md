# Flowfield — a living shader

A real-time WebGL generative aurora, rendered entirely in a fragment shader.
Move your pointer to stir the flow; click to send a pulse rippling through it.

**Zero dependencies. One file. No build step.**

## Run it

## Live 
https://frenzelferrer.github.io/Flowfield/

Open `index.html` in any modern browser — that's it. It also works served from
any static host.

## Deploy it

Any static host works. The easiest options:

- **GitHub Pages** — push this folder to a repo, then
  `Settings → Pages → Deploy from a branch → main / (root)`.
  Live at `https://<username>.github.io/<repo>/`.
- **Netlify Drop** — drag the folder onto [app.netlify.com/drop](https://app.netlify.com/drop).
- **Vercel / Cloudflare Pages** — import the repo; auto-deploys on every push.

## Controls

| Action | Effect |
|---|---|
| Move pointer | Stirs the field, swirling the flow around you |
| Click / tap | Emits a pulse ring through the field |
| `Nebula · Ember · Aurora` | Crossfades between three color moods |
| ⏸ button | Pauses / resumes the animation |

Leave it alone for a few seconds and an autonomous drift takes over,
so the field keeps breathing on its own.

## How it works

- A single fullscreen triangle runs a fragment shader with **five octaves of
  domain-warped gradient noise** (`fbm(p + fbm(p + fbm(p)))`).
- Pointer position and velocity feed a **swirl uniform** that locally rotates
  the sample domain — the "ink in water" feel — plus a decaying pulse ring on click.
- The three moods are three-stop color palettes blended in the shader, so
  switching moods crossfades smoothly.
- Rendering is capped at `devicePixelRatio ≤ 2`, pauses when the tab is hidden,
  and uses `powerPreference: 'low-power'`.

## Accessibility & theming

- Follows the OS **light / dark** preference (`prefers-color-scheme`).
- Honors **reduced motion**: renders a single still composition instead of
  animating; pointer and mood changes re-render one frame at a time.
- Full keyboard access and ARIA labeling on all controls; the canvas carries a
  descriptive `role="img"` label.
- Graceful fallback message when WebGL is unavailable.

## License

MIT — do whatever you like with it.
