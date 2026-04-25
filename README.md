# AI-Powered Tailored Resume Generator

An intelligent system designed to create highly customized, ATS-optimized resumes and cover letters by aligning a candidate's master profile with specific job descriptions.

## 🚀 Features

### 🎯 Intelligent Tailoring
- **JD-Driven Content Selection**: Automatically analyzes the Job Description (`JD/JD.md`) to extract key requirements and company information.
- **Dynamic Project Selection**: Selects the two most relevant projects from the candidate's profile that best match the target role.
- **Truthful Keyword Injection**: Naturally integrates JD keywords into existing achievements without fabricating experience or metrics.
- **Relevance-Based Reordering**: Reorders experience bullets to prioritize the most relevant accomplishments for the specific job.

### 🛠️ Professional Document Generation
- **LaTeX Integration**: Uses a professional LaTeX template (`format/template.tex`) and custom class (`format/resume.cls`) for high-quality PDF output.
- **ATS Optimization**: Follows strict guidelines for ATS readability, including a specific project format and a competency grid of 6-8 keyword phrases.
- **Automatic Compilation**: Handles the full pipeline from content generation to PDF compilation using `pdflatex`.
- **Cover Letter Generation**: Generates a professional cover letter in `.docx` format tailored to the company and role.

### 🛡️ Ethical & Quality Guardrails
- **Strict Truthfulness**: Built-in constraints prevent the invention of experience, metrics, or the use of "corporate-speak."
- **Source of Truth**: Maintains a strict separation between the master profile (`Profile/candidate-profile.yaml` and `Profile/cv.md`) and the generated outputs.
- **No Fabrication**: Ensures that all claims in the tailored resume are grounded in the candidate's actual history.

## 📂 Project Structure

- `Profile/`: Contains the source of truth for the candidate (YAML profile and Markdown CV).
- `JD/`: contains the target job description (`JD.md`).
- `format/`: LaTeX templates and styling definitions.
- `modes/`: Logic and guidelines for different generation modes (e.g., PDF/ATS optimization).
- `output/`: Organized by company name, containing the final `.tex`, `.pdf`, and `.docx` files.

## ⚙️ Workflow

1. **Prepare Inputs**: 
   - Update `Profile/candidate-profile.yaml` with your latest experience.
   - Paste the target job description into `JD/JD.md`.
2. **Generate**: 
   - Run the `/resume-generator` skill.
3. **Review**: 
   - Find your tailored documents in the `output/[company_name]/` directory.

## 🛠️ Technical Stack

- **AI Orchestration**: Tailored prompting and content analysis.
- **Formatting**: LaTeX (`pdflatex`).
- **Data Format**: YAML, Markdown.
- **Output**: PDF, DOCX.
