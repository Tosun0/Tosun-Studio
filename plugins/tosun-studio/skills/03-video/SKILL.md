---
name: 03-video
description: Produce or validate Tosun videos by invoking the connected Higgsfield plugin and collecting real generation results for approval.
---

# Video

Work only on the video sequence. Master-Tosun owns state changes and approval.

- Read only approved storyboard motion fields, approved source images, and required media settings.
- Discover and invoke the connected Higgsfield plugin. Do not use a paid API, browser automation, request artifact, or another provider as a silent substitute.
- Default to Kling 3.0 Pro (`model: kling3_0`, `mode: pro`) unless the user selects another model. Set `sound: on` for storyboard dialogue; preserve the requested duration and aspect ratio.
- Inspect the live model constraints and call `estimate_video_cost` with the exact generation settings before submission. Report the credit quote; do not hard-code prices. Connected-plugin generations spend Higgsfield credits, while the standalone REST API has separate billing.
- Reuse the user's approved model, settings, and cost without asking again. If the quote exceeds the authorized cost or a required setting must change, resolve that change with the user before spending credits.
- Submit one bounded generation per cut when separate clips are required. Preserve character identity and avoid motion or anatomy deformation.
- Use `count: 1` for each cut. Record the returned job ID immediately; never automatically resubmit after an ambiguous timeout or switch to a more expensive model.
- Wait for the provider's real completion state and collect the actual returned media result.
- If Higgsfield returns a local media file, copy it into project artifacts without overwriting the source. If it returns only a hosted result, display it and do not claim a local file exists.
- Validate actual decoding, duration, resolution, frame rate, codec, and audio presence when applicable.
- Do not claim a requested frame rate from the prompt or model name. Inspect the output; preserve the original and report any conversion needed for delivery.
- If Higgsfield is missing, disconnected, rejected, or returns no media, report `waiting_external` or `failed`.
- Stop after the real video is displayed and validated. Master-Tosun must record explicit approval before routing to `remotion`.
