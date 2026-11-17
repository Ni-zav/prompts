# Image-to-video prompt builder: Seedance 2.5 and Higgsfield Genjutsu

**Verified:** 2026-11-17. **Use:** Turn an image (and optionally a motion-reference video) into model-specific, copy-ready production prompts. This is a reusable **prompt to make prompts**, not a guarantee of video-model fidelity.

## Choose the right workflow first

| Task | Seedance 2.5 | Higgsfield Genjutsu |
| --- | --- | --- |
| Animate one still image | Use image-to-video with the still as first/reference frame | **Not available from the still alone**; requires a source video |
| Define new camera motion in words | Yes; specify one restrained camera move | No; source video's camera and timing guide the output |
| Re-create a scene using motion from a clip | Use a supported reference-video workflow where offered | Use **Motion Transfer** plus scene/reference images |
| Change one object in an existing clip | Use edit mode if available | Use **Object Swap**, not Motion Transfer |

Higgsfield officially documents a **4–30-second** source video plus reference images for Genjutsu, and describes **Motion Transfer** versus **Object Swap**. Interface controls, limits, costs, and model behavior may vary by provider or date; confirm them in the target UI. Seedance 2.5 guidance from Dreamina and Krea recommends scene/action + camera + timing + reference roles + audio + constraints. These are prompting guidelines, not an immutable syntax.

## Copy-paste: the reusable prompt-to-prompt generator

~~~text
I will supply a still image and may also supply a reference video. Produce production-ready VIDEO prompts tailored separately for (1) Seedance 2.5 and (2) Higgsfield Genjutsu.

My optional inputs:
- Objective: [cinematic aerial / architectural flythrough / product / other]
- Image: [attached image]
- Reference video for Genjutsu: [attached video or NONE]
- Duration: [6 s by default]
- Output ratio: [match original by default]
- Preferred camera movement: [one simple move or recommend]
- Required motion: [e.g. physically plausible traffic, water, leaves]
- Forbidden changes: [e.g. new buildings, changed layout, altered identities]
- Audio: [off / natural ambience / specific audio]
- Priority: [maximum geometry fidelity by default]

Before prompting:
1. Inspect the provided image; describe its ACTUAL composition and visible anchors: foreground/background, location of structures, architecture, roads, shore, vehicles, water, lighting, perspective, and horizon. Do not guess the exact city or invent unseen details.
2. Divide elements into (a) rigid/invariant geometry, (b) naturally moving elements, and (c) permissible camera/parallax motion.
3. Choose a physically coherent camera movement. For a reference still with distinctive buildings or road topology, prefer a small stabilized move over a sweeping orbit. Preserve a consistent 3D world across all frames.
4. Distinguish observation from assumption. Never claim a clip was tested unless there is actual evidence.

For SEEDANCE 2.5:
- Treat the still as the starting/reference image.
- Write one concise, copy-ready prompt describing: what to preserve -> moving elements -> camera path -> duration/timing -> light/look -> audio -> exclusions.
- Use one primary camera move and modest environment motion. Specify accurate scale, perspective, vehicles on road surfaces, and coherent motion when relevant.
- A fixed opening composition, continuous single take, and stable end frame are preferable for architectural image-to-video.
- Avoid restating the entire still or stacking incompatible camera moves.

For HIGGSFIELD GENJUTSU:
- Check whether there is a source video. If NONE: clearly label the prompt CONDITIONAL — SOURCE VIDEO REQUIRED; provide the *type* of matching source clip needed, rather than pretending an image alone will run.
- Choose Motion Transfer when the goal is to apply the source clip's motion/camera/timing to a location or scene defined by the image. Choose Object Swap only if one selected object in the source clip is meant to change.
- Write a brief edit instruction in this order: CHANGE from reference image -> KEEP from source video -> LOCK fixed elements/realism. Do not instruct Genjutsu to invent a different camera movement than the supplied clip.
- For geographically detailed architecture, warn that a mismatched camera angle or large reveal can require unseen geometry and cause reconstructions to drift. Prefer reference footage with compatible angle, speed, path, duration, and composition.
- Do not claim to preserve geometry perfectly or imply source video is optional.

Return:
A. Observed scene inventory (short; image facts versus assumptions).
B. Seedance 2.5: settings and a copy-paste generation prompt.
C. Genjutsu: selected mode, required video type, setup and a copy-paste edit prompt; explicitly conditional if no video was supplied.
D. Five-item quality checklist tailored to the image and one-variable-at-a-time fixes for the most likely artifacts.
Make the two prompts materially different, not the same paragraph with different model names. The default aesthetic is natural photorealism; avoid generic "epic masterpiece" filler.
~~~

## Worked example: coastal high-rise aerial photograph

**Source image:** a 2048 × 1152 (16:9) high-angle aerial of a densely built coastal peninsula, with a curved seaward multi-lane coastal road on the left, a rocky breakwater and white surf, clustered mid/high-rise apartment towers in the center, greenery and street grid, calmer inlets/harbor water at the rear/right, distant port infrastructure, bright hazy daylight. **Do not assert a geographic identity.**

**Invariants:** Peninsula outline; exact relative tower count/positions/heights; roads and lane markings; breakwater rocks; coastline, harbors, trees, overall daylight and lens perspective. **Motion:** slow small cars/buses in their actual lanes, gently changing water/surf, slight tree movement; camera parallax kept modest.

### Seedance 2.5 — direct image-to-video

**Suggested setup:** attached still = first image; 6 s; 16:9; single continuous take; natural audio or off; start with 720p or 1080p depending on the provider and budget.

~~~text
Use the supplied aerial photograph as the exact opening frame and visual blueprint. Create a 6-second, single-take photorealistic drone shot. The drone makes a very slow, stabilized forward glide toward the central high-rise cluster, holding nearly constant altitude, heading and framing; only subtle true-to-depth parallax occurs. Preserve the exact peninsula silhouette, curvature and width of the coastal divided road, number and arrangement of towers, tree masses, shoreline rocks, harbor basins, distant port and bright hazy daytime lighting. Animate only believable real-world movement: a few properly sized vehicles traveling steadily within their existing lanes, with consistent left-hand traffic where the carriageways indicate it; soft ocean ripples and small white wave breaks against the rocks; minimal leaf motion. Perspective, road surfaces, vertical building edges, shadows and water boundaries remain stable. No camera rotation, no cuts, no time-lapse, no added architecture, no melted buildings, no warped roads, no sliding cars, no exaggerated waves. Finish on a stable frame. Audio, if enabled: very faint coastal wind/surf and distant road ambience; no music or dialogue.
~~~

### Higgsfield Genjutsu — motion transfer (conditional)

**Prerequisite:** provide a separate **4–30 s source video**, ideally a 6-second stabilized high-angle aerial of a coastal/urban peninsula with a similar starting perspective, gentle forward glide and no sudden pan or orbit. Attach the photograph as a **location/scene reference**. This is **not** an executable image-only prompt. Select **Motion Transfer**, not Object Swap. If using your Seedance output as the source video, Genjutsu becomes a refinement/rebuild experiment rather than a necessary first step; assess added value before spending credits.

~~~text
MOTION TRANSFER. Rebuild the source video's landscape and architecture to match the supplied coastal-peninsula reference image: the same curved divided seaside road and rock breakwater along the left, dense central group of residential towers with consistent individual heights and spacing, green tree belts, calm harbor and inlets at the right and rear, and hazy bright daytime color and materials. KEEP the uploaded source video's exact 6-second shot duration, smooth aerial forward movement, camera pitch, framing rhythm and natural motion pacing; do not introduce an orbit, zoom or new cuts. LOCK the reference image's recognizable coastline, road geometry, tower arrangement and scale as closely as the moving perspective permits. Road vehicles must remain small, follow their lanes and travel consistently with left-hand traffic; water and coastal surf move subtly. Aim for physically plausible drone realism, stable buildings and coherent parallax. No extra towers, invented islands, roads that bend or shift, vehicle sliding, fantasy effects or sudden weather changes.
~~~

**Practical caution:** Genjutsu uses the actual source clip to determine motion and may redraw the scene. A single still cannot establish unseen facades and viewpoints. Strong orbiting/panning footage is therefore a poor match for a strict replication request.

## Quality-control checklist

1. **Architecture:** first and last frames retain the same identifiable tower layout, building counts and silhouette; no facade or roof melts.
2. **Topology:** shore, breakwater, divided road, lanes and harbor boundaries stay contiguous; no new bridges/roads.
3. **Traffic:** size and speed match a high-altitude aerial; vehicles stay on asphalt, obey lane directions, never teleport or drive backward.
4. **Physics:** water moves gently with foam at rocks, no drifting land masses; parallax follows scene depth and shadows remain consistent.
5. **Shot:** single smooth camera path, no jump cut, jerk, random zoom, dramatic day/night change, flicker or unstable end frame.

**If a test fails:** Change only one major control per retry. First reduce camera displacement; then reduce number of moving elements; then shorten duration; then choose a better matched source video (Genjutsu). An explicit constraint helps but cannot guarantee perfect geometry. Compare frame 0 / middle / end at equal size.

## Sources consulted (2026-11-17)

- [Higgsfield: How do I use Genjutsu?](https://higgsfield.ai/creator-hub/help-center/tools/how-do-i-use-genjutsu) — official, 2026-10-26; modes, video requirement, references, prompting.
- [Higgsfield Genjutsu product page](https://higgsfield.ai/genjutsu) — official source-video motion and object-swap workflow.
- [Dreamina: Seedance 2.5 prompt guide](https://dreamina.capcut.com/seedance/seedance-2-5-prompt) — subject, action, camera, duration, audio, continuity, negative constraints.
- [Krea: Seedance 2.5 prompt guide](https://www.krea.ai/blog/seedance-2-5-prompt-guide) — guide published 2026-10-26, sequence and camera vocabulary.

No paid renders or controlled head-to-head tests were performed for this contribution. Recommendations are workflow design grounded in docs and the supplied still, not verified model output.
