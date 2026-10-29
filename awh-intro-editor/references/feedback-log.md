# Hassan intro editor feedback log

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

## 2026-10-11 — First `personal` build on the ported compositor; inherited jump cuts

Affected artifact: `edit/client-1-intro` (new project). No existing master changed.
Hassan chose `personal`, confirmed the on-screen name spelling, and approved
the beat plan as proposed. These are build-side lessons, not new preferences from Hassan.

- **Whisper can drop a phrase without leaving a gap.** The full pass dropped "that
  too in simple words with examples" and "why would you use it". No segment gap
  marked either one, because a neighbouring word ("GPT") was stretched over 1.4 s to
  cover the hole. So check words longer than about 0.8 s as well as segment gaps.
  When unconditioned re-pass windows overlap, remove the duplicate word at each seam.
- **A card's shadow counts toward the corridor.** A 140 px paper shadow carried
  the alpha footprint 128 px past the card edge, into the presenter corridor. Size
  cards to the corridor including their shadow, and use the compositor's
  `overlay_bbox` to read the real footprint.
- **The card surface must not lead its first line.** The card's ease front-loads
  opacity, so a surface that starts two frames before its title reads as an empty
  white box. Start both on the same frame.
- **Never hold an empty surface while waiting for a spoken number.** Show the
  number's resting state faintly (a counter at 0) from the card's arrival, then
  run it so it lands on the spoken figure.
- **A full-screen reveal must not begin while the panel is still sliding.** A
  9-frame fade ending on the word started inside the slide. The eyebrow and rule
  should travel with the panel. The hero word should snap in from the word onset
  after `landed`.
- **Locked cuts carry jump cuts, and the spike check must allow for them.** The
  frame-difference spike test flagged ratios of 2.9 and 3.5 at 6.81 s and 20.95 s.
  The source had the same diffs (5.88 and 9.09), and the master matched them to
  within 0.02. `verify_master.py` now measures the source over each window and
  excludes spikes the source already has (master within 10% of source).
- **Re-rendering a frame range.** `remotion render --frames=a-b --sequence` names
  frames without zero padding (`element-200.png`). Rename them to the track's
  4-digit scheme before swapping them in.
- **Personal theme on the compositor.** The inset canvas is plain warm paper
  (`#F5F3EE`), and the inset and edge shadows use ink `#151922`. Avenir Next loads
  from macOS system fonts in headless Chrome, so no web font is needed.

Application policy: standing for future videos.

## 2026-10-11 — Official logos for every mentioned brand

Affected artifact: the skill, for future videos. No existing master changed.

Hassan asked: "always get official logo if a company or brand is mentioned and use that."

There was no failure on a specific render. This is an explicit standing preference. The gap it closes: brands could appear as typed names or generic icons, and the stock-icon ban could be misread as covering logos.

Correction and reusable lesson:

- List every company, brand, product, and tool named in the transcript or on-screen copy before designing graphics.
- Fetch each official logo from the brand's own press kit, brand page, or website. Never redraw, recolor, or stand in with text or a generic icon.
- Store the files under `edit/<project>/assets/logos/` and record them in the directive's `brand_logos` with source URL, retrieval date, and SHA-256. `validate_directive.py` now checks each file exists and matches its hash.
- An unconfirmed logo is an approval ambiguity, so ask Hassan instead of falling back silently.

Promoted to `brand-system.md` under "Brand and company logos", to `SKILL.md` as workflow step 3, and to `editorial-directive.md`.

Application policy: standing for future videos.

## 2026-10-13 — GitHub screen recording for every repo or open-source tool

Affected artifact: the skill, for future videos. First applied to `edit/sponsor-2-skills-intro`. No existing master changed.

Hassan asked: "when a github repo or opensource tool is mentioned, add its github screen recording or screenshot at that point to the editing visual."

There was no failure on a specific render; this is an explicit standing preference. The gap it closes: an open-source tool could appear only as a logo or a typed name, and viewers never saw the real project they are being sent to.

Correction and reusable lesson:

- List every GitHub repo and open-source tool named in the transcript or the on-screen copy.
- Confirm the official upstream repo through the public GitHub API (not a fork, homepage, license). Mirrors and look-alikes don't count.
- Capture it live and logged out with `scripts/capture_repo.py` (2×, light scheme, tall clip for scrolling).
- Show it in a browser window with the real URL at the moment it is named, with a camera that moves to what the narration describes.
- Record it in the directive's `repo_captures`. `validate_directive.py` checks the files and hashes, and warns when a beat says "GitHub" or "open source" without a capture.
- Check the narration against the repo page. On the first video, the narration said Sponsor 7 gives "1.6 billion tokens daily", but its README says "~1.62B tokens / month". A contradiction like that is an approval ambiguity, not something to render silently.

Promoted to `brand-system.md` under "GitHub repos and open-source tools", to `SKILL.md` as workflow step 4 and an editorial rule, and to `editorial-directive.md`.

Application policy: standing for future videos.

Build-side lessons from the first repo edit (`edit/sponsor-2-skills-intro`):

- **Never mount a whole page capture.** A 3216×13200 px GitHub page in one `<Img>`, decoded in every Chrome tab, grew macOS swap past 5 GB and filled the disk to 0 bytes. Every tool failed, even a shell `df`. `capture_repo.py` now writes 1600 px tiles with a 2 px overlap, `RepoBrowser.tsx` mounts only the tiles in view, and renders run at `--concurrency=4`. With these changes a still renders in seconds, and the full 1740-frame track used 1.1 GB with no swap growth.
- **GitHub markup moves.** `#repo-stars-counter-star` no longer exists. Find the title and the Star button by their visible text near the top of the page.
- **Product mark vs parent mark.** sponsor-7.example shows its parent company's mark. The product's own icon in its official repo is the logo to use.
- **A card right after a full-screen panel loses its fade-in.** The panel owns every frame up to one past its window. A card whose fade started three frames earlier was hidden under it, then appeared at 79% opacity in one frame. The verifier caught this as a 4.48 frame-diff spike at the panel exit. Start the fade no earlier than two frames after the beat begins. When that squeezes the fade, use a symmetric smootherstep over about 11 frames, because the front-loaded entrance ease jumps half-way in a single frame.

## 2026-10-13 — Re-recorded Sponsor 1 intro; build-side timing lessons

Affected artifact: `edit/sponsor-1-intro/sponsor-1-intro2` (new project). The intro1 edit is unchanged.

Hassan re-recorded the intro and asked for a from-scratch edit with the latest skill, saved inside the Sponsor 1 folder. Theme `warner` was carried over from his 2026-10-09 choice for this video. These are build-side lessons, not new preferences from Hassan.

- **Typed card titles collide with the next speech-synced row when the card has to open late.** Here the card could only open after the cut's own collage cleared (5.40 s), and the next row lands at 5.92 s, but a 25-character title takes 1.4 s to type. When a card's first row lands sooner than the title can finish typing, fade the title in instead.
- **Long typed headlines lag the speech.** At 1.7 frames per character, a 33-character headline typed from the panel landing finished 1.6 s after its spoken word. Split it: the part already spoken before the landing becomes an eyebrow that travels with the panel, and a shorter remainder is typed.
- **A card next to a panel must end before the panel's headroom frame** (`panelFrames().first`, one frame before the window). The panel path owns that frame, and any card pixels in it slide away with the panel.
- **Your own campaign frames beat abstract tiles.** When the cut already shows the creator's real ads, lossless crops of those tiles make the "ad variants" visual authentic. Record them in `assets/SOURCES.json` as derived from the locked cut.
- **Low disk without symlinks:** when the pinned `package.json` and lockfile are identical to another project's, `cp -c -R` (an APFS clone) of its `node_modules` costs no disk and stays independent if the original is deleted.

Application policy: standing for future videos.

## 2026-10-13 — Theme prompt skipped on the sponsor-1-intro2 re-edit

Affected artifact: `edit/sponsor-1-intro/sponsor-1-intro2`.

Hassan: "when did you ask me about the edit style?"

Observed failure: the edit went straight to `warner` without the theme prompt that workflow step 1 requires. The reasoning was that he had chosen warner for intro1 of the same video. He had asked for the re-edit "from scratch", and a previous project's choice is not a choice for this one.

Reusable lesson: ask the theme question at the start of every project, including re-records, re-edits and later sections of a video that already has a theme. Present the earlier choice as the suggested default, but ask.

Application policy: standing for future videos.

## 2026-10-24 — sponsor-6-short (9:16 Short, circle inset)

- **Review of rev 0:** "its TOP!", with one change: the circle inset framed only the face.
- **Request:** "zoom out a little … add some shoulders as well, so as much as one can see in a passport style photograph."
- **Fix:** the crop window went from a 1000 px face square (centre y 800) to the full 1215 px crop width (centre y 830). It now shows the hair with a margin, the collar and the upper shoulders.
- **Lesson:** frame a presenter circle as a passport photo by default (head plus shoulders), not as a tight face crop.
