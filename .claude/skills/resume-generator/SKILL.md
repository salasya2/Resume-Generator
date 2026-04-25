---
name: resume-generator
description: AI agent based Tailored Resume Generator
user_invocable: true
args: mode
---

# resume-generator

## Step 0 — Parallel Pre-Load (do this FIRST, before anything else)

**Read all of the following files simultaneously in a single batch** (do not wait for one before starting the next):

| File | Path |
|------|------|
| cv.md | `Profile/cv.md` |
| candidate-profile-gen.yaml | `Profile/candidate-profile-gen.yaml` |
| JD.md | `JD/JD.md` |
| template.tex | `format/template.tex` |
| resume.cls | `format/resume.cls` |
| pdf.md | `modes/pdf.md` |
| single.md | `modes/single.md` |

If `JD/JD.md` is missing or empty, stop and alert the user immediately.

## Step 1 — Mode Routing

Determine mode from `{{mode}}`:

| Input | Mode |
|-------|------|
| (empty / no args) | `single` — execute single resume generation |

## Step 2 — Execute

Proceed with the pipeline defined in `modes/pdf.md` using data already loaded in Step 0.
Do not re-read any file that was already read in Step 0.

