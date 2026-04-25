# Mode: pdf — ATS-Optimized PDF Generation

## Full Pipeline

1. Read `cv.md` as the source of truth
2. Ask the user for the JD if it is not already in context (text or URL)
3. Detect company location -> paper format:
   - US/Canada -> `letter`
4. Detect role archetype -> adapt framing
5. Select the top 2 most relevant projects for the role, Only use two most relevant projects from `candidate-profile-gen.yaml`
6. In the project sections use this **exact** LaTeX pattern (mirrors EXPERIENCE style):
   ```latex
   \textbf{Project Name} \hfill Mon YYYY -- Mon YYYY\\
   Tech1 $\cdot$ Tech2 $\cdot$ Tech3
    \begin{itemize}
       \itemsep -3pt {}
     \item Description bullet.
    \end{itemize}
   ```
   **CRITICAL**: `\cdot` requires math mode — always write `$\cdot$`, never bare `\cdot` in text. Do NOT use `rProjectItem` or `rProjectSection` environments.
7. Reorder experience bullets by JD relevance
8. Build a competency grid from JD requirements (6-8 keyword phrases)
9. Inject keywords naturally into existing achievements (NEVER invents)
10. **DO NOT generate a Professional Summary / Objective section. Skip it entirely.**
11. Before compiling, **copy `format/resume.cls` into `output/{company}/`** so pdflatex can find it:
    - Windows: `copy format\resume.cls output\{company}\resume.cls`
    - Linux/Mac: `cp format/resume.cls output/{company}/resume.cls`
12. Run pdflatex **once** with `-interaction=nonstopmode` and `-output-directory` so all auxiliary files land in the right folder (a single pass is sufficient — resumes have no TOC or cross-references):
    `pdflatex -interaction=nonstopmode -output-directory output/{company} output/{company}/cv-candidate-{company}.tex`

## ATS Rules (clean parsing)

- 


## Keyword Injection Strategy (ethical, truth-based)

Legitimate rewriting examples:
- JD says "RAG pipelines" and CV says "LLM workflows with retrieval" -> change to "RAG pipeline design and LLM orchestration workflows"
- JD says "MLOps" and CV says "observability, evals, error handling" -> change to "MLOps and observability: evals, error handling, cost monitoring"
- JD says "stakeholder management" and CV says "collaborated with team" -> change to "stakeholder management across engineering, operations, and business"

**NEVER add skills the candidate does not have. Only rephrase real experience with the exact JD vocabulary.**
