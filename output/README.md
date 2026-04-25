# Output Directory

This directory contains generated resumes and cover letters, organized by company name.

## Structure
```
output/
├── [company_name]/
│   ├── cv-candidate-[company].tex     # LaTeX source
│   ├── cv-candidate-[company].pdf     # Generated PDF resume
│   └── cover-letter-[company].docx    # Generated cover letter
```

## Usage
- Generated files are automatically organized by company name extracted from the job description
- Each company gets its own subdirectory containing the tailored resume and cover letter
- Files are named consistently for easy identification