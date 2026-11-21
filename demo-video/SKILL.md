---
name: demo-video
description: Make a scripted product or investor demo video (about 60-90 s, 1080p) from real code, real API output and measured benchmarks, by rendering an HTML composition with Hyperframes.
---

# Demo video with Hyperframes

Use when the user wants a demo, brag or investor video of a software project. The video is an HTML page with timed animations rendered to MP4. Content must come from the real running project, not mock-ups.

## 1. Decide the audience first
- Clients: short (about 25 s), outcomes, UI, a simple story.
- Investors: about 60-90 s, how it works: architecture, real code, real API request and response, database rows, measured performance, risks.
- Ask one question only if unclear; otherwise pick and say which.

## 2. Collect real evidence (before any design)
1. Run the real project locally (real database, real server).
2. Capture a real API request and response and save it to a file.
3. Write a benchmark script that goes through the real API (for example 100 enrolments, 400 verifies). Record median, p95, p99, accept/reject counts and the test-suite pass count.
4. Pull real code excerpts, database rows and constants (retry/backoff, encryption).
5. Note caveats honestly (synthetic data, simulated integration, untested live service) and show the main one on screen.
6. Fictional names only.

## 3. Plan scenes (about 8-11, 6-11 s each)
Hook -> what it replaces -> architecture with a travelling packet -> core code typed out -> live request/response -> integration code -> database rows -> measured performance -> risks -> outro. Keep a cuts list of scene start times; music and sound effects are timed from it.

## 4. Build the composition
- Generate composition/index.html from a Python script so timings change in one place. Set data-duration. 1920x1080.
- GSAP animation, attribute-driven: .a with data-at, code lines .cl with data-type="start,step", word masks for headings.
- Text at least 28 px, one idea per scene, footer pills must not overflow.
- Background music plus short sound effects at each cut.

## 5. Check and render
```
export HYPERFRAMES_BROWSER_PATH=/usr/bin/google-chrome   # without it the render fails: no Chrome
npx hyperframes@0.9.41 check
npx hyperframes@0.9.41 render
```
Fix every check error (overlap, small text, clipped tiles, clipped code lines). data-layout-allow-overlap only for intended overlaps. 77 s renders in about 3 min. Extract one frame per scene with ffmpeg and look at a grid before delivering.

## 6. Removing or re-ordering scenes
Rebuild the cuts array and the sound-effect timings from the new scene list; patching single numbers leaves effects off by one. Re-run check, then render.

## 7. Deliver
- Full MP4, poster JPG, benchmark JSON and composition source in brag-output/<name>/.
- For upload limits make a compact copy (720p, under about 3.8 MB for the Chrome extension file_upload).
- Upwork portfolio: the built-in browser cannot drive native file pickers, so the user uploads the video once; fill the other fields and publish.
- State plainly what was measured and what was not.
