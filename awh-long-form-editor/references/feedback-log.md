# Hassan long-form editor feedback log

## 2026-09-08 — Initial preferences

- Preserve native 4K quality and avoid unnecessary downscaling or aggressive compression.
- Motion graphics must feel professionally directed, never absurd, generic, or visibly AI-generated.
- Cards and text must not cover the presenter's face or interfere with meaningful gestures.
- Use the warm-paper, ink, muted gray, fine-line, cobalt, and Avenir Next design language from `Personalized_AI_Roadmap_Presentation.html`.
- Create complete full-screen motion-graphic sequences at selected semantic intervals, while retaining presenter footage between them.
- Build a timestamp-driven editorial directive before creating graphics so treatment selection follows meaning rather than arbitrary timing.
- Preserve natural audio and complete thoughts; visual activity does not justify an audio cut.

## 2026-09-08 — Connector geometry correction

Observed failure: the `IDEA → WORKING POC` overlay used a malformed or crowded connector. The arrow shaft/head competed with the right-hand label and read as overlapping strokes.

Reusable lesson:

- Reserve an explicit gap between connected labels before drawing the connector.
- Keep connector geometry simple and inspect the encoded result at native resolution.
- Animate node, shaft, and destination in sequence; never let the arrowhead collide with text.
- When space is tight, prefer a clean line-and-node progression over a decorative arrow.

Implementation result in `personalized-ai-roadmap-intro-v2`:

- Promoted the correction into the standing brand system under “Diagram geometry.”
- Rebuilt the moment as a full-screen transformation rather than a crowded presenter overlay.
- Reserved x=1510–2050 exclusively for the connector, with at least 130 px between that channel and each card.
- Native 3840×2160 inspection confirmed that the connector does not touch either label or card.

## 2026-09-08 — V2 baseline approved

Hassan reviewed `personalized-ai-roadmap-intro-v2` and described it as “PERFECT” for the current iteration. Treat this edit as the approved baseline for future intros.

Reusable lesson:

- Preserve the V2 balance between clean presenter moments, face-safe overlay cards, selective text, and purposeful full-screen motion.
- Keep the locked presentation-derived palette and typography unless Hassan explicitly requests a change.
- Retain the directive-first workflow and semantic reveal timing.
- Do not infer or lock unspecified future improvements; record them only when Hassan identifies them.

## 2026-09-08 — Full-screen numbering and brand signature

Observed issue: full-screen animations included decorative sequence labels such as `01 / 04`, `02 / 04`, and similar numbering. Hassan stated that this does not look nice and must not be used.

Standing standard:

- Never add slide, scene, page, or sequence numbering to full-screen animations unless Hassan explicitly asks for it.
- Remove decorative step numbers when they are not required by the narration or meaning.
- Add the exact wordmark `AI with Hassan` to the upper-right of every full-screen animation.
- Keep that signature fixed in the same position and visual treatment across all full-screen scenes.

Application policy:

- Apply this standard to future videos; the currently approved V2 master remains unchanged.
- Implement the signature as a shared full-screen frame element so every future full-screen scene inherits it automatically.

## Update policy

Append new feedback with the date, affected artifact, observed issue, correction, and reusable lesson. Promote a lesson into `brand-system.md` when Hassan states it as a standing preference or when it recurs. Preserve historical entries instead of rewriting them.

## 2026-09-10 — Final-cut input, presenter inset, and directional entrances

Affected artifact: personal editing skill for future videos; no existing master changed.

Hassan clarified: “i give you a final cut (you dont need to edit and remove cuts), only edit with animation, motion graphics etc.” He requested: “animate and move my entire video to one corner in a transition stlye while in the screen you animate what you want” and “for full screen animations, they should come from right swipe or top/bottom.”

Observed workflow mismatch: the prior explanation included take selection and cutting even though the supplied video is already edited. The visual vocabulary also lacked a presenter inset and a standing directional entrance rule.

Correction and reusable lesson:

- Lock supplied final-cut timing and audio; use transcription only to synchronize visuals.
- Add `PRESENTER_INSET`: smoothly move and scale the entire video into a corner while an explanatory animation fills the remaining space, then return to full frame.
- Use right, top, or bottom slide/wipe entrances for full-screen motion, choosing direction intentionally.
- Record layout and entrance/exit decisions in the directive. These are available treatments and entrance rules, not mandatory usage percentages.

## 2026-09-11 — Inset transition mechanics, border visibility, pacing, and type scale

Affected artifact: `edit/sponsor-4-intro` V2 master and the skill; rules promoted to `brand-system.md`.

Hassan's review of the first inset build: “The transition from full screen to small screen is horrible, this should be smooth. Its terrible.” He confirmed the settled inset size was right and the vertical slide entrances were good, then asked for rounded corners and a border on the inset, roughly 20% more animation because “there are scenes where nothing happens for long duration,” and a slightly larger, still professional type scale. On the follow-up he added that the new border was not visible.

Observed issues:

- The inset used `transformOrigin: 'top left'` while also animating `left`/`top`. The two motions compounded, so the left edge travelled 2400 px while the right edge moved 160 px and the picture collapsed sideways rather than tucking into the corner.
- The easing was a cubic ease-in-out, which concentrated travel at the midpoint: 277 px in a single frame, while the picture was simultaneously shrinking.
- The first border used the `line` tone `#d7d4cc`, measured at (214,210,201) against a (229,226,223) paper background — invisible.
- 26% of graphics runtime sat beyond comfortable reveal spacing, including a 4.9 s gap in `api`, a 4.4 s lead-in in `employee`, and a 5.0 s static tail in `chat`. Every element faded in over ~0.45 s and then held perfectly still.
- Body text at 78–86 px on a 4K canvas is roughly 36–40 px at 1080p, small for phone viewing.

Correction and reusable lesson:

- Scale about the picture's centre and move that centre along one path; never pair a corner transform origin with animated offsets.
- Use smootherstep for the inset move and verify peak per-frame travel rather than trusting the curve name.
- Keep radius and border weight constant on screen by dividing by the current scale.
- Use `#737985` for the inset border; `#d7d4cc` vanishes on warm paper.
- Derive the graphics fade from the transition duration so the two cannot drift apart.
- Raise liveliness with entrance snap, overshoot, arrival accents, and post-landing drift, never by moving narration-synced reveals.
- Grow containers, row pitch, and connector spans whenever type grows, and re-inspect at native resolution.

Application policy: applied to the V2 rebuild of `sponsor-4-intro`; standing for future videos.

## 2026-09-12 — Multi-theme architecture (`personal`, `black-circle`, `warner`) & typewriter pacing

Affected artifacts: `brand-system.md`, `SKILL.md`, `editorial-directive.md`, `scripts/validate_directive.py`.

Context & User Request:
Hassan tested reference styles and directed:
1. Support 3 distinct visual themes:
   - `personal` (Hassan Signature: warm paper `#F5F3EE`, cobalt `#3659E3`, ink `#151922`, Avenir Next).
   - `black-circle` (Hybrid: light grey `#F5F5F5` canvas, neon lime `#E8FF72`, rotating 8-spoke black flower wheels, un-bold Avenir Next).
   - `warner` (Warner Classy: engineering grid `#EEF1F6`, royal navy `#1D2070`, golden amber `#FEAF1D`, un-bold classy typography @ 48px, enlarged corner floating spheres, dual-tone line icons).
2. Update the skill workflow so that whenever it is invoked, it first prompts the user to select which theme to use before proceeding.
3. Fix typewriter stalls and adjust typography aesthetics:
   - Corner geometric balls: scale up to 350px (Navy `r=142`, Amber `r=115`) with organic micro-floating drift (`±5px`).
   - Typewriter animation: eliminate the final-letter stall caused by cubic ease-out truncation; use steady linear character pacing (`1 char / ~1.7 frames`) landing cleanly on the final character.
   - Un-bold classy typography: bold (`700/800`) is not always required and can look heavy. For sophisticated executive presentations, use un-bold medium weight (`fontWeight: 500` / `600`) paired with larger font size (`48px` / `76px`).

Reusable lesson & standing standards:
- Always prompt for theme selection upfront on every new project.
- Implement theme selection into the directive schema under `"theme": "personal" | "black-circle" | "warner"`.
- Maintain kinetic secondary motion across themes (e.g. continuous rotation on `black-circle` wheels, organic micro-drift on `warner` corner spheres).
- Never use ease-out curves that flatten near completion for character-by-character typewriter reveals.

Application policy: Promoted into standing brand system; available across all future intro edits.

## 2026-09-20 — Replaced source under the same filename; inset audit caught a regression

Affected artifact: `edit/sponsor-4-intro-v3` (new project). No existing master changed.

Context: Hassan said "I have added my intro, edit the final video using my
skill." The root `sponsor-4-intro.mp4` had been replaced that day and was now
60.59 s, while `edit/sponsor-4-intro/` had been built on 2026-09-10 from a 101.6 s
file of the same name (SHA `c37fa3c7…` vs the new `5852e644…`).

Observed risk: the previous directive's beat timestamps were silently invalid
against the new cut. Re-using them would have desynchronised every reveal
without any error surfacing.

Reusable lesson:

- Hash the source before reusing any directive. A matching filename is not a
  matching cut. When the hash differs from the one recorded in the project's
  directive, the timestamps are stale — re-derive them, and ask whether this is
  a fresh project or a re-time before touching anything.
- Re-measure the presenter corridor per video rather than inheriting the
  documented `x=1600`. Sampling ~30 frames and taking the per-pixel luminance
  range produces a motion map that locates the corridor objectively; on this
  footage it independently reproduced `x=1600`, and it also revealed that the
  hands cross into the lower-left, which needed a second protected region.
- The peak-per-frame-travel check on the inset path earns its keep. The first
  timing here (1.10 s in / 0.75 s out) audited at 254.7 px/frame — close to the
  277 px/frame move Hassan rejected on 2026-09-11 — and was caught before
  rendering, not after review. 1.30 s in / 1.10 s out audits at 174 px/frame.
  Always measure; never trust the curve name.
- `drawbox`'s `t` (thickness) is already in output pixels, i.e. on-screen space.
  Dividing it by the current scale — correct for a CSS border on a scaled
  element — would inflate the border as the picture shrinks. The 1/scale
  division applies to weights authored in the *picture's* coordinate space, not
  to filters that draw in output space.
- FFmpeg expression portability: `clip()` is unavailable in the scale/overlay/
  drawbox evaluators, and `overlay` exposes the timestamp as lowercase `t` only
  (it rejects `T`, unlike some other filters). Write ramps with `min/max` and a
  single `t`, and verify the closed-form expressions against the reference path
  numerically before committing to a render.
- Verify alpha semantics mechanically, not by eye: extract the alpha plane at a
  card beat and assert `max(alpha[:, 1600:]) == 0` for the presenter corridor,
  and assert `max(alpha) == 0` across a `CLEAN_PRESENTER` beat. This proves the
  face-safe and visual-silence guarantees in the encoded file rather than in
  layout arithmetic.

Application policy: standing for future videos.

## 2026-09-20 — Inset transition ghosting, one-frame jump, and text without a surface

Affected artifact: `edit/sponsor-4-intro-v3` master (rev 2). Rules are general.

Hassan's review: "the big to small video transition is buggy… Also there is
another card that does not work correctly… make the transitions from big to
small video and small to big seamless."

Observed issues — none of them were the inset motion itself, which audited
correctly at 174 px/frame throughout:

- **Double-compositing.** The Remotion graphics track painted its own opaque
  canvas with a `clipPath` hole at the *settled* inset rectangle, and the FFmpeg
  segment underneath already supplied canvas + moving picture + border. The
  canvas covered the genuinely moving picture while the fixed hole revealed a
  second, wrongly-placed copy; the hole's edge read as a static box over the
  footage.
- **One-frame blank at the switch.** The segment's background came from a
  separate `color` source, which carries its own timebase. `overlay`'s first
  output frame therefore had the canvas but not yet the per-frame `scale`
  output, so frame 0 of the beat was bare canvas — measured as "only the
  wordmark present" — and read as a jump cut into the move.
- **Border shown too early.** Gated at `p>0.02`, the frame appeared while the
  picture was still near full-size, floating over the footage.
- **Text with no surface.** `SELECTIVE_TEXT` is the one treatment with no card
  behind it. Its headline sat on the light wall (bg mean 164) but the sub-line
  crossed the dark monitor (bg mean 125, darks at 27), so black type there was
  effectively invisible.

Reusable lessons:

- **One layer owns the canvas.** When a beat is composited across two stages
  (FFmpeg footage transform + an alpha graphics track), exactly one of them may
  paint the background. Cutting a hole in the second one to "let the picture
  through" only works while the picture is at the hole's position — during a
  move it is not, so it ghosts. The graphics track should stay transparent and
  contribute graphics only.
- **Never build a moving composite's background from a separate `color`
  source.** Derive it from the input stream (`split` then
  `drawbox=...:thickness=fill`) so both branches share a timebase. A separate
  source desynchronises by a frame at the boundary, and a single blank frame is
  clearly visible as a jump.
- **Verify a transition by measuring the picture's extent per frame**, not by
  looking at a contact sheet. Measuring width against the expected curve caught
  both the blank frame (3840 expected, wordmark-only found) and confirmed the
  fix (3840 → 940 in, 924 → 3840 out). Note that a "non-background bounding box"
  measure picks up graphics too — measure the photo by colour saturation when
  graphics share the frame.
- **Gate a picture frame/border on the transform's progress,** not merely on the
  beat window. Below roughly `p>0.35` the picture still reads as full-frame and
  a border around it looks like a stray rectangle.
- **Text placed directly on footage needs a measured background.** Sample the
  luminance under *each line's* band, not the block as a whole: the same card
  can have a legible headline and an illegible sub-line. Below ~120 mean, black
  type needs a plate. Size the plate to the type, not the full card, and
  re-check the presenter corridor afterwards (it stayed at alpha 0 here).
- **FFmpeg `drawbox`: use the long form `thickness=`.** The short `t=` collides
  with the `t` timestamp variable used in its own `w`/`h` expressions and the
  filtergraph fails to parse.

Application policy: standing for future videos.

## 2026-09-25 — First `warner` build; transcription gap, disk, and frame-count lessons

Affected artifact: `edit/sponsor-3-intro` (new project). No existing master changed.
Hassan chose `warner` and approved the beat plan without changes. These are
build-side lessons, not new preferences from Hassan.

- **Whisper can silently skip a passage.** The full pass dropped 20.70–30.00 s
  (the Google/Reddit/Amazon/eBay list) with no error. Check the segment list for
  gaps longer than about 2 s against `silencedetect`. Re-transcribe any gap
  window on its own with `condition_on_previous_text=False` before syncing
  reveals.
- **Check free disk space before a 4K ProRes 4444 render.** A 60 s track is
  about 1.9 GB, and Remotion's faststart step writes a second copy. VP9
  `yuva420p` (CRF 12) held full alpha at 11 MB and kept text crisp at native
  4K. Read it with `-c:v libvpx-vp9` before `-i`, because the native vp9
  decoder drops alpha.
- **`overlay` repeats its last frame at EOF.** Lock the frame count with
  `trim=end_frame=N` inside the filter graph. Output `-frames:v N` also
  truncates the stream-copied audio tail, which breaks bit-identical audio.
- **Measure the inset by its border, not by saturation.** Low-saturation walls
  made a saturation probe under-read the settled inset by 90 px. Locating the
  `#737985` border is exact.
- **Warner in practice.** The upper-right wordmark and the top-right sphere pair
  compete for the same corner. Seat the pair below the nav bar and partly
  outside the right edge so both circles show. Keep content at least 100 px
  clear of the amber disc.

Application policy: standing for future videos.

## 2026-10-06 — Ghost box on the inset return; single-pass compositor

Affected artifacts: `edit/sponsor-5-intro` (new project). The diagnosis was made
on `edit/sponsor-3-intro`'s master; that master was not changed.

Hassan: "i sometimes notice a bug when the video gets back to normal (big size)
after becoming smaller, please make sure its seamless when floating small and
also when going back to big. transitions should be seamless."

Observed failure (frame-by-frame on sponsor-3-intro, 39.0–40.6 s and 24.1–25.7 s):
a thin `#737985` rectangle sat frozen at the settled inset position while the
picture grew back to full frame (and while it shrank on the way in). Cause:
`drawbox` evaluates its x/y/w/h expressions once, and inside those expressions
`t` is the box **thickness**, not time. The "animated" border was a static box
that only coincided with the picture during the hold. The 2026-09-20 note that
`t=` "collides with the timestamp" misread this. The geometry was never per-frame.

Reusable lesson:

- **Do not draw moving inset chrome with `drawbox`.** Render picture, corner
  radius, border and shadow from one per-frame geometry in a single compositor
  (`edit/sponsor-5-intro/scripts/composite.py`). They then cannot disagree.
- **Chrome is a function of inset progress, not of the beat window.** Radius,
  border and shadow ramp in with progress and are exactly zero at full frame,
  so the first and last frames of each move equal the untouched footage. Verify
  this against the source, not by eye.
- **No splice.** Pass every frame through the same decode → composite → encode
  path. The swscale bt709 RGB round trip measures Y 72 / U 56 / V 70 dB, which is
  invisible, so an `enable=between()` segment swap is unnecessary and risky.
- **Sub-pixel motion and motion blur.** `scale` + `overlay` quantise position
  and size to whole pixels. Area pre-scale plus a sub-pixel warp removes the
  stair-step, and a 180° shutter (sub-samples for scale moves, translation blur
  for slides) makes 140–164 px/frame read as smooth.
- **Shutter headroom frames must not be composited in place.** Rendering the
  full-screen panel one frame either side of its window (for the shutter) would
  flash the whole panel for one frame if those frames were treated as ordinary
  overlays. The compositor routes the whole window through the slide path.
  This was caught on preview before the master render.
- **Regression tests for this class of bug:** frames just outside each move must
  match the source; the settled-inset perimeter must not carry a border-coloured
  outline mid-move; consecutive-frame difference must have no single-frame
  spike across each transition.
- **Remotion sequence output:** `--sequence` rejects any output path containing
  a dot, including `..` and the user's home directory. Render to a
  dot-free relative folder and move it.
- **Opaque PNG frames lose their alpha channel.** Treat 3-channel frames as
  fully opaque when loading.

Application policy: standing for future videos. Promoted into `brand-system.md`
under "Presenter inset and directional entrances".

## 2026-10-09 — Source with its own graphics; dangling shared dependencies

Affected artifact: `edit/sponsor-1-intro` (new project). No existing master changed.
Hassan chose `warner` and approved the beat plan as proposed. These are
build-side lessons, not new preferences from Hassan.

- **A locked cut can already carry graphics.** `sponsor-1-intro1.mp4` opens with
  an ad-sample collage in the top-left (0.97–3.84 s). Scan the source for
  existing overlays (a per-frame diff of the card region against a later clean
  frame finds them exactly) and start cards after they clear. The directive
  validator has no time-scoped protected region, so record such a window in the
  beat's purpose and the treatment instead of `protected_regions`.
- **Whisper skipped half the intro again** (21–47 s collapsed into one line).
  The gap re-pass with `condition_on_previous_text=False` remains mandatory.
- **Do not symlink `node_modules` to another project.** Every earlier project
  pointed at `five-step-framework/animations/node_modules`, which has since been
  deleted, so none of them can re-render. Install per project from the pinned
  `package.json`.
- **Read the spike ratio at its frame.** A ratio near the 1.8 limit can come
  from the graphics fade-in on the first frame after an inset lands, not from
  the picture. Locate the peak frame and compare its absolute diff with the
  move's own peak before acting.

Application policy: standing for future videos.

## 2026-10-11 — Forked from `hassan-intro-editor`

Affected artifact: this skill (new). `hassan-intro-editor` is unchanged.

Hassan created this skill as a copy of `hassan-intro-editor` to develop and
test long-form editing without risking the approved intro editor. The entries
above were inherited at the fork and describe intro projects; keep them as
history. Record long-form feedback here from now on. It does not flow back to
the intro editor unless Hassan asks for that explicitly.

Application policy: standing for future long-form videos.

## 2026-10-11 — `dark-sketch` theme from a reference recording

Affected artifacts: `brand-system.md`, `SKILL.md`, `scripts/validate_directive.py`
in this skill only. `hassan-intro-editor` is unchanged.

Hassan asked to add one more style, copied from
`Screen Recording 2026-10-11 at 09.40.50.mov` (60.4 s, 4080×2298, no audio).

How the style was measured, so it can be re-checked:

- Colours were sampled from full-resolution frames: canvas `#181A1C` (flat at
  every corner and the centre), ink `#E2E2E2`, blue fill `#578AE0`, blue text
  `#6792D1`, orange `#CB9370`.
- The typeface was identified by rendering Shantell Sans beside the reference.
  It matches glyph for glyph (J with a top bar, I with serifs, f descending
  below the baseline). Weight 700. Sizes were derived from measured cap and
  ink heights against the font's own metrics.
- The motion was measured per frame. From 7.9 s onward every change completes
  within a single frame: bullets, statements, the underline, diagram labels,
  code, and colour changes all appear instantly, and slides swap as hard cuts.
  Holds between builds run 1.2–6.2 s (median 2.5 s). Between topics the
  canvas cuts to empty for 1.3 s (50.0–51.3 s). The first 7 s are player
  scrubbing and were excluded.

Decisions taken to fit the standing rules (open to change after testing):

- The instant builds and static holds are kept as the theme's own motion
  grammar, which overrides the general secondary-motion rules for this theme
  only. A hold longer than about 6 s gets a narration-synced build, not drift.
- Hassan's slide/wipe entrance rule and the inset mechanics still apply at the
  boundary between footage and the full-screen canvas. The reference shows no
  footage, so it says nothing about that boundary.
- The `AI with Hassan` wordmark is kept, restyled in Shantell Sans with the
  theme's blue and ink.

Application policy: available to future long-form videos as `dark-sketch`.

## 2026-10-11 — Warm paper theme, corner moves, and audio-only sections

Affected artifacts: `brand-system.md`, `SKILL.md`, `editorial-directive.md`,
`scripts/validate_directive.py` in this skill only. `hassan-intro-editor` is
unchanged.

Hassan compared three sketch-style options in `outputs/sketch-style-options.html`
and chose option B: "for now lets do b (warm paper)". He kept the proposed
section rhythm and added: "when my video becomes smaller as floating, move it
every now and then to other corners to make it look interactive, for some
sections i will only provide audio so that animations take full screen".

Standing standards:

- `warm-paper` is the default theme for long-form. Theme selection is still
  offered at the start of each project.
- Long-form uses a section rhythm: full-frame for trust moments, inset for
  longer explanations, full-screen for short focus moments.
- A floating inset moves to another corner now and then, at natural breaks,
  as a pure translation. In the sketch themes the title and wordmark occupy
  the top corners, so moves run between bottom-left and bottom-right.
- Audio-only sections are assembled into the locked program and are fully
  covered by full-screen graphics.

Decisions taken (open to change after testing): corner holds of at least about
20 s; the 960×540 inset with 120px margins approved in `sponsor-1-intro`;
per-segment loudness matching proposed in the directive rather than applied
silently.

Application policy: standing for future long-form videos.

## 2026-10-11 — client-1-1: tutorial-angle camera, never full-frame

Affected artifact: `edit/client-1-1` (new project, the first long-form section after
`edit/client-1-intro`), plus `scripts/validate_directive.py`.

Hassan: "add a relevant filter frame around my footage and never put me 100% on
the screen (because the angle i recorded is only good for tutorial style where i
look largely at the other screen), also quality is not exceptional (direct from
macbook pro camera), rest adjust accordingly and give me final edit".

What was done, and the reusable lessons:

- **Tutorial-angle footage stays in a framed window throughout.** The
  presenter is never full-frame. A window moves between named states (a large
  "stage" beside a text column, the bottom-right corner, and off-canvas for
  full-screen graphics). Each move is one smootherstep path with the size changing
  about the centre. The verifier proves the paper is visible in the frame corners
  on every frame.
- **Place the window on the side the presenter faces.** Hassan looks
  screen-left, so the window stays right and he appears to look at the
  graphics. A move to a left corner would make him look out of the frame. With
  gaze this one-sided, movement comes from size and position changes instead of
  corner swaps. This was flagged to Hassan for review.
- **Never upscale a weak camera.** A 1080p source on a 4K canvas is capped at
  1920×1080 (1:1) in its largest state.
- **Frame and filter.** The warm-paper card frame (white mat, ink outline,
  concentric radius, no shadow) is constant on screen. A restrained corrective
  grade was chosen from a two-option side-by-side test (light hqdn3d, pink cast
  pulled, contrast +5%, saturation -8%, mild unsharp).
- **Match the previous section's loudness.** client-1-1 was 2.8 LU quieter than the
  intro master. Gain plus a peak limiter matched it to -14.7 LUFS. Record this in
  the directive's `audio` block.
- **Turn off code ligatures.** JetBrains Mono rendered `>=` as `≥`. Code on
  screen must read exactly as typed, so ligatures are off in the warm-paper spec.
- **Source and delivery can differ.** The 59.94 fps 1080p camera is delivered at
  29.97 fps 4K to match the intro (output frame i = source frame 2i). The
  validator now reads `delivery.width/height` for layout bounds instead of the
  source size.

Application policy: applies to the remaining client-1 sections recorded with the same
camera setup. Do not generalise "never full-frame" to footage that faces the
camera unless Hassan asks.

## 2026-10-11 — client-1-1 review: "filter frame" means a mask that removes dead space

Affected artifact: `edit/client-1-1` (master v1 stays as delivered). Mask variants are
in `edit/client-1-1/variants/`, with samples in `renders/samples/`.

Hassan: "When you create a bigger recording of me (and also when it becomes
small), i asked you to setup a filter which masks extra space that does nothing.
you did not do it."

Observed failure: "relevant filter frame" was read as a border plus a colour
grade. The window still showed the whole 16:9 frame, roughly half of it empty
wall and door.

Reusable lesson:

- **A "filter frame" around Hassan's footage is a crop mask in a shape**
  (circle, portrait card, soft fade, and so on) that removes dead space at
  every window size. A border and a grade alone are not enough.
- **Derive the crop from measured head positions, not from a single frame.** A
  Haar frontal and profile face pass over the whole section, at 3 fps, gives p1–p99
  extents. Keep the crop static, so there is no floating camera, and check that the
  head never leaves it.
- **Cap the upscale at 1.2x** when cropping a weak camera, so the crop can
  still fill a stage-sized shape.
- **When the brief is ambiguous, offer 2–3 short samples** (5 s, including a
  resize move) instead of committing a full render.

Application policy: Hassan picks one of the three masks; it then becomes the
standing frame for the client-1 sections recorded with this camera.

## 2026-10-11 — client-1-1 review 2: the corner window was too small

Hassan, on the mask samples: "when you move it to bottom corner, it think it
becomes very small. it can be slightly bigger."

Correction: the corner went from 540 to 690 px high on the 4K canvas (about +28%,
1.6x the area). Treat a corner height of roughly 690 px as the floor for masked
presenter windows. Size it from the measured graphics clearance (the lowest
corner-side graphic pixel plus 80 px), not from the old 960x540 default, and
reflow nearby graphics upward if they block it.

## 2026-10-11 — client-1-1 review 3: circle chosen, an even bigger corner, code in an IDE window

Hassan: "lets do circle, i still think the small side could still be slightly
bigger when in corner ... When showing code on screen if easy, build a terminal
or IDE style window which makes it look fancier."

Standing standards, promoted to `brand-system.md` (warm-paper):

- **Presenter mask:** a circle, about 1200px at the stage size and 800px in the
  corner (540 → 690 → 800 across the reviews). To make room, the graphics were
  reflowed: the "How do you code this?" message column was raised by 100px in total.
- **Code:** a dark IDE-style window with window dots, a file tab, line numbers
  and meaning-lit tokens.

Hassan also asked to delete every test clip, variant and superseded client-1-1 render
once the circle was chosen. Keep project folders free of superseded media;
the project log keeps the history.

## 2026-10-11 — client-1-2: brand icons, and one folder for all sections

Hassan, handing over the second section: "use the same idea and logic as for
client-1-1 edit, and save it under client-1-1 (dont create separate folders for each).
also one more thing, when a brand is mentioned, fetch its latest icon image
from internet and use that."

Standing standards:

- **Brand icons:** when the narration names a brand, show that brand's current
  icon, fetched for the project, instead of a drawn stand-in or a text-only label.
  Promoted to `brand-system.md` under "Brand icons".
  - Check that it is the *latest* mark. Amazon's 2012 logo on Wikimedia was
    retired in the 2025 refresh, so the current logo came from aboutamazon.com.
  - Prefer the brand's own site icon or SVG. When the site blocks automated
    downloads (openai.com, chatgpt.com and claude.ai do), use the Wikimedia
    Commons file of the current mark.
  - Record the source, retrieval date, hash and any recolouring in a
    `SOURCES.json` beside the files.
- **Sections share one project folder:** a series recorded in sections lives in
  one `edit/<project>/` folder with shared scripts and Remotion code. The first
  section keeps the plain file names. Later sections add a `-<section>` suffix
  (`timeline-client-1-2.json`, `renders/client-1-2-4k.mp4`), and the scripts select a
  section with `CLIENT_1_SECTION`.

## 2026-10-18 — agentic-ai-system-design voice-overs 2-3: no black-circle wheels (one-off)
- Hassan: "remove the black circles at left top and bottom right corner … just for these audios, dont edit the first audio again or dont change the skill theme."
- Applied per project only (directive `"ornaments": "none"`). Not promoted to brand-system.md; the `black-circle` theme keeps its wheels.

## 2026-10-20: rag-crash-course section 2 (theme change mid-series)
- Hassan: "ask me about theme or style, i dont like the first style that much, i might change this time." He chose black-circle for section 2 and to leave section 1 in warm-paper.
- Lesson: a series' theme is not fixed. When a new section arrives, ask the theme again and offer the last one as the default.
- He chose "no wheels" again (the second project after agentic-ai-system-design). That makes it a repeated preference. It is not yet promoted, because he said earlier not to change the skill theme; ask him whether black-circle should drop the wheels by default.

## 2026-10-20: rag-crash-course section 1 re-themed, section 3 added
- Hassan: "edit rag-crash-course-3.m4a and update rag-crash-course-1.m4a using the theme that is used to edit rag-crash-course-2.m4a." Section 1 was rebuilt from warm-paper to black-circle without wheels (`Segment1.tsx`, same cues); the warm-paper master is kept as `rag-crash-course-1-warm-paper-4k.mp4`.
- This is the third time he has picked black-circle without wheels, and the second time he has moved off warm-paper. It is still not promoted (see the 2026-10-20 entry above); ask him whether to make it the default.

## 2026-10-24 — crumpled-paper theme sample (edit/crumpled-paper-theme)
- Grey headline line → make it black. Paper texture was too loud: background should be white or only a very faint texture. Green highlights (note text, callout pill) needed better font and colour; rev 2 uses richer green `#1e7b46` notes and a lighter mint pill with Fredoka 600 in deep green `#17462b`. Not yet promoted to brand-system.md (theme still in review).
