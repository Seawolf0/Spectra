# Spectra

**A real-time light-physics playground that runs in the browser.** Spectra has two modes: a 3D spectral path tracer and a 2D optics "light table". It's a single HTML file with no libraries, no build step and no installs.

![3D mode: Crystal cathedral preset, with tinted glass casting colored light across the floor](docs/3d.jpg)

![2D mode: Rainbow in a raindrop preset, with light bending through a water drop into rainbow bows](docs/2d.jpg)

Spectra started as an experiment in what a frontier AI model can build from a detailed prompt. **Claude Fable 5.2** (Anthropic) generated most of the code from prompts I designed and refined. I tested each version, dug into the code to track down bugs, fixed some of them by hand, and directed every change.

---

## Try it

- **Online:** [seawolf0.github.io/Spectra](https://seawolf0.github.io/Spectra/)
- **Locally:** download `index.html` and open it in Safari or Chrome.

It requires a desktop browser with **WebGL2** and floating-point render targets. A recent Safari or Chrome on a Mac works well, and it was developed on an Apple Silicon MacBook Pro.

## Modes

### 3D: progressive spectral path tracer
A studio scene with a curved backdrop, filled with glass and metal objects and lit by up to three lights. All rendering happens in a fragment shader.

- **Spectral rendering:** paths carry real wavelengths (about 380 to 700 nm), and wavelength-dependent refraction splits white light into a rainbow (dispersion).
- **Glass and metal:** Fresnel reflection and refraction, total internal reflection, Beer–Lambert absorption for tinted glass, and spectral metal reflectance.
- **Caustics:** a GPU photon map projects focused light from the glass onto the floor.
- **Visible beams:** photon paths are drawn through a haze layer, so you can see the beam in the air.
- **Fast convergence:** next-event estimation with multiple importance sampling for the studio lights.
- **Camera:** thin-lens depth of field, with double-click to focus.
- **Color pipeline:** CIE color matching to sRGB, ACES tone mapping and bloom.
- **Denoiser:** an edge-aware à-trous filter, guided by depth, normals and surface color, cleans up the image at low sample counts and fades out as the render converges. Low-discrepancy sampling and an adaptive firefly clamp help it converge faster.
- **Progressive refinement:** the image refines toward a clean, unbiased result when still. A "Show raw samples" toggle turns the denoiser off. The resolution adapts to keep interaction smooth.
- **Objects:** a glass prism, sphere, faceted crystal, cube, biconvex lens and brilliant-cut diamond, plus a polished metal ring, a flat mirror and a back wall that catches spectra.
- **Lights:** up to three, each a white spot (with color temperature), a colored light or a monochromatic laser.

**Controls:** light angle, elevation, beam width and aim; color temperature, studio fill and haze; dispersion, refractive index, tint and tint density; aperture and focus distance; bounces, exposure and resolution. Click an object to select it and drag it across the floor.

**Presets (14):** *Pink Floyd prism*, *Caustic pool*, *Crystal cathedral*, *Cardioid*, *Diamond fire*, *Burning glass*, *Rainbow sphere*, *RGB shadows*, *Laser show*, *Trapped light*, *Spectrum on the wall*, *Stained glass*, *Macro*, *Moonlight*.

### 2D: spectral light table
A top-down optics bench. You build setups and watch tens of thousands of spectral rays per frame flow through them.

- **Optics:** convex and concave lenses, prisms, glass blocks, glass balls, curved glass strips, flat and curved mirrors, absorbing walls and diffuse surfaces.
- **Light sources:** white laser, flashlight, point light and a monochromatic laser with a wavelength control.
- **Light detector:** measures how much light, and what color, reaches it.
- **Editing:** move, rotate and scale with handles, plus undo/redo, duplicate, delete and arrow-key nudging.
- **Per-object glass settings:** refractive index and dispersion.

**Presets (13):** *Newton's prism*, *Rainbow in a raindrop* (primary and secondary bows), *Fiber optic* (total internal reflection), *Telescope* (a Keplerian refractor), *Concave mirror focus*, *Periscope*, *Chromatic aberration*, *Achromatic doublet*, *Microscope*, *Lighthouse lens*, *Laser maze*, *Kaleidoscope*, *Dispersion showdown*.

Both modes share the spectral color pipeline and the PNG screenshot button. Presets are grouped by theme (Refraction, Reflection, Colour, Optics and Showcase), each with a one-line note on the physics.

## Learning tools

- **Guided tour:** opens on your first visit and walks through the main controls, with each card placed next to the control it explains. The Tutorial button in the top bar restarts it.
- **Challenges:** 18 short tasks across both modes, from aiming a single laser to building anything you like. Each one unlocks only the controls it needs, checks your progress live with light detectors, and saves your progress in the browser.

## Version history

| Version | What changed |
|---|---|
| **1.0** | First build: 3D path tracer and 2D light table, with three and four presets |
| **2.0** | Denoiser and faster sampling, a curved studio backdrop, five new 3D objects, up to three lights, 20 new presets, a guided tour and 18 challenges |

More versions are coming, starting with sound and a cinematic intro.

## How it was made

1. I wrote prompts describing the goal, the physics, the interaction and the quality bar.
2. Claude Fable 5.2 (high thinking) produced the full program from each prompt.
3. I tested every version in the browser and went into the code when something broke. Some issues, like the 3D noise, went back to Fable as follow-up prompts. Others I fixed by hand.

## License

All rights reserved for now.
