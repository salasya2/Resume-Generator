# System context  resume-generator

<!-- ============================================================
     THIS FILE IS AUTO-UPDATABLE. Don't put personal data here.
     
     Your customizations go in modes/_profile.md (never auto-updated).
     This file contains system rules, scoring logic, and tool config
     that improve with each career-ops release.
     ============================================================ -->

## sources of truth

| File | Path | When |
|------|------|------|
| cv.md | `Profile/cv.md` (project root) | ALWAYS |
| candidate-profile-gen.yaml | `Profile/candidate-profile-gen.yaml` | ALWAYS (candidate identity — lean version, use this instead of candidate-profile.yaml) |
| JD.md | `JD/JD.md` | ALWAYS (Job Description) |
| pdf.md | `modes/pdf.md` | ALWAYS (PDF Generator) |
| template.tex | `format/template.tex` | ALWAYS (Resume Template) |
| resume.cls | `format/resume.cls` | ALWAYS (Resume Template) |

**These files are pre-loaded in Step 0 of SKILL.md. Do NOT read them again.**


## RULE: Make sure to alert the user if the JD file is absent
## RULE:  use `modes/pdf.md` to understand the rules.
## RULE: Make sure to not make up information and use the information from `cv.md` and `candidate-profile.yaml`
## RULE: Create a cover letter using the resume generated and the JD
## RULE: Avoid putting address of the company in the cover letter, and cover letter must be of the '.docx' format.
## RULE: Always store the generated resumes in `output/`, create a folder `{{company_name}}` and store  the Resume and cover letter in that folder.


## Global Rules

### NEVER

1. Invent experience or metrics
2. Modify cv.md or portfolio files
3. Generate a PDF without reading the JD first
4. Use corporate-speak
5. Skip creating a cover letter