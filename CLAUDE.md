# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an AI-powered Tailored Resume Generator that creates customized resumes and cover letters based on:
- Candidate profile (`Profile/candidate-profile.yaml`) 
- Master CV (`Profile/cv.md`)
- Job Description (`JD/JD.md`)
- LaTeX template (`format/template.tex` and `format/resume.cls`)

The system extracts relevant information from the candidate's background and tailors it to match specific job descriptions while maintaining truthfulness and avoiding fabrication of experience.

## Key Files and Directories

### Core Configuration
- `Profile/candidate-profile.yaml` - Full candidate profile (human-readable, source of truth — do not modify)
- `Profile/candidate-profile-gen.yaml` - **Lean generation profile** (commentary fields stripped; this is what the agent reads — ~40% smaller)
- `Profile/cv.md` - Master CV in markdown format (source of truth for experience)
- `JD/JD.md` - Target job description (required for resume generation)

### Templates and Styling
- `format/template.tex` - Main LaTeX template for resume generation
- `format/resume.cls` - Custom LaTeX class file defining resume structure and styling

### Output
- `output/` - Generated resumes and cover letters organized by company name
  - Structure: `output/[company_name]/cv-candidate-[company].tex/.pdf` and `cover-letter-[company].docx`

### Mode Definitions
- `.claude/skills/resume-generator/SKILL.md` - Main skill definition
- `modes/single.md` - Single resume generation mode (default)
- `modes/pdf.md` - PDF generation rules and ATS optimization guidelines

## Common Commands

### Resume Generation
The primary way to interact with this system is through the resume-generator skill:

```bash
# Generate a tailored resume (default single mode)
/resume-generator

# Or explicitly specify single mode
/resume-generator single
```

### Development Commands
These commands are permitted in the settings and useful for development:

```bash
# Compile LaTeX to PDF (used internally by the system)
pdflatex output/[company_name]/cv-candidate-[company].tex



# File operations
ls -la output/
dir output*
```

### Workflow
1. Ensure `JD/JD.md` contains the target job description
2. Run `/resume-generator` to generate tailored resume and cover letter
3. Generated files appear in `output/[extracted_company_name]/`
4. The agent automatically copies `format/resume.cls` into the output folder before compiling
5. PDF is compiled via: `pdflatex -interaction=nonstopmode -output-directory output/[company] output/[company]/cv-candidate-[company].tex` (single pass only)

## Important Rules and Constraints

### Truthfulness Guidelines (from modes/single.md)
- **NEVER** invent experience or metrics
- **NEVER** modify `cv.md` or portfolio files  
- **NEVER** generate a PDF without reading the JD first
- **NEVER** use corporate-speak
- **NEVER** skip creating a cover letter

### PDF/ATS Optimization (from modes/pdf.md)
- Uses only the two most relevant projects from candidate-profile.yaml
- Injects JD keywords naturally into existing achievements (never invents)
- **Does NOT generate a Professional Summary / Objective section**
- Projects section: use `\textbf{Name} \hfill Date\\` + tech stack line + `\begin{itemize}` bullets (see `modes/pdf.md` step 6 for the exact pattern). **NEVER** use bare `\cdot` in text — always `$\cdot$`. Do NOT use `rProjectItem` or `rProjectSection`.
- Reorders experience bullets by JD relevance
- Builds competency grid from JD requirements (6-8 keyword phrases)
- For US/Canada locations: uses letter paper format

### File Naming and Organization
- Company name is extracted from the JD for folder naming
- Spaces in company names are converted to underscores for file compatibility
- All generated files go to `output/[company_name]/` directory
- Resume: `cv-candidate-[company].tex` and `.pdf`
- Cover letter: `cover-letter-[company].docx`

## Architecture Summary

The system operates in a deterministic pipeline:
1. **Input Processing**: Reads candidate data (YAML + MD) and JD
2. **Content Tailoring**: 
   - Extracts company name from JD
   - Selects top 2 relevant projects (rendered as itemized bullets)
   - Reorders experience by JD relevance
   - Injects keywords truthfully
   - **Skips Professional Summary section entirely**
3. **Document Generation**:
   - Copies `format/resume.cls` into `output/[company]/` before compiling
   - Populates LaTeX template with tailored content
   - Compiles to PDF via pdflatex (`-output-directory` flag keeps all files in the output folder)
   - Generates DOCX cover letter
4. **Output Organization**: Files stored in company-named subdirectories

The system emphasizes ATS optimization while maintaining strict ethical boundaries against fabricating qualifications.