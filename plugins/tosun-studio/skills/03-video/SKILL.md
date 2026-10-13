---
name: 03-video
description: Produce or validate Tosun videos by invoking the connected Higgsfield plugin and collecting real generation results for approval.
---

# Video

Work only on the video sequence. Master-Tosun owns state changes and approval.

- Read only approved storyboard motion fields, approved source images, and required media settings.
- Discover and invoke the connected Higgsfield plugin. Do not use a paid API, browser automation, request artifact, or another provider as a silent substitute.

## Before a paid request

- Default to Kling 3.0 Pro (`model: kling3_0`, `mode: pro`) unless the user selects another model. Set `sound: on` for storyboard dialogue; preserve the requested duration and aspect ratio.
- For dialogue, prepare the speaker-to-line mapping from the approved storyboard and source image before quoting or submitting. Identify each speaker by visible position, clothing or another stable visual feature, and role; a role such as `father` alone is insufficient when several people share the frame. Resolve unclear identity instead of guessing.
- For Korean dialogue, default to a Korean scene prompt. Preserve every spoken line verbatim. Put the speaker's position and visual identity directly beside each line, with its speaking interval and the listener's closed-mouth reaction. Separate turns with a brief pause and give each line enough time; do not rely on a shared dialogue block or a final `do not swap speakers` sentence.
- For everyday dialogue, keep gestures small and motivated by the scene. Add large hand movements, theatrical delivery, narration, extra dialogue, or captions only when supported by the storyboard or requested.
- Compare the final prompt with the approved source: every line has the correct speaker, the speaking intervals do not overlap, the dialogue fits the duration, and the reference composition and requested settings are preserved. Save this mapping and the prompt with the existing request artifact before spending credits. This is a prompt check, not a guarantee of the generated result.
- Inspect the live model constraints and call `estimate_video_cost` with the exact generation settings before submission. Report the credit quote; do not hard-code prices. Connected-plugin generations spend Higgsfield credits, while the standalone REST API has separate billing.
- Reuse the user's approved model, settings, and cost without asking again. If the quote exceeds the authorized cost or a required setting must change, resolve that change with the user before spending credits.

## Generation and revision

- Submit one bounded generation per cut when separate clips are required. Preserve character identity and avoid motion or anatomy deformation.
- Use `count: 1` for each cut. Record the returned job ID immediately; never automatically resubmit after an ambiguous timeout or switch to a more expensive model.
- After a rejected result, record the user's exact issue, the affected speaker or action, and the concrete prompt change before a retry. Preserve previous requests and results. Use explicit regeneration authorization: one request within the approved settings and budget unless the user has authorized a different count or retry budget. Do not spend credits to test speculative variants.
- If the same dialogue failure recurs, explain the remaining uncertainty before another paid attempt. Splitting shots, separate voice or lip-sync work, or changing models must follow the user's scope and cost decision.
- Wait for the provider's real completion state and collect the actual returned media result.
- If Higgsfield returns a local media file, copy it into project artifacts without overwriting the source. If it returns only a hosted result, display it and do not claim a local file exists.

## Review and handoff

- For individual-cut delivery, follow the master's [delivery layout](../00-master-tosun/references/delivery-layout.md). Return the exact submitted prompt and generation facts for that cut; do not scatter prompt packs or per-attempt notes at the delivery root.
- Unless the user takes over verification, validate actual decoding, duration, resolution, frame rate, codec, and audio presence when applicable. For dialogue, also check the audible line against the visible speaker and mouth movement; a transcript alone cannot establish who spoke.
- When the user says they will verify, carry that choice through retries and record `not_run`. Report provider completion without claiming that speech, speaker assignment, or lip sync is correct. An explicit user assessment is recorded as user review, separately from agent verification.
- Do not claim a requested frame rate from the prompt or model name. Inspect the output; preserve the original and report any conversion needed for delivery.
- If Higgsfield is missing, disconnected, rejected, or returns no media, report `waiting_external` or `failed`.
- Stop after the real video is displayed with the verification outcome or the user's verification opt-out. Master-Tosun must record explicit approval before routing to `remotion`.
