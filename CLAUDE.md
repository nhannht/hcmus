# CLAUDE.md

Academic workspace for Nguyen Huu Thien Nhan (nhannht), HCMUS Education Technology program.

## Student Info

- **Student ID:** 25310023
- **Git:** `nhannht` / `nhanclassroom@gmail.com` / https://github.com/nhannht

## Directory Structure

All courses are individual GitHub repos (FISHcmus org) added as git submodules.

```
hcmus/
├── profile/                  # FISHcmus/.github org profile (submodule)
├── semester1/                # Semester 1 (2025-2026) — 6 course submodules
│   ├── calculus-1/
│   ├── general-chemistry-1/
│   ├── intro-edtech/
│   ├── intro-marxism-leninism/
│   ├── linear-algebra/
│   └── marxism-economic/
├── semester2/                # Semester 2 (2025-2026) — 5 course submodules
│   ├── intro-oop1/           # OOP1 — C++14, raylib Caro project
│   ├── intro-edu-science/    # Nhập môn KHGD
│   ├── science-socialism/    # CNXHKH — has own CLAUDE.md
│   ├── probability-statistics/ # Xác suất thống kê (MTH00044)
│   └── history-vcp/          # Lịch sử Đảng CSVN
├── hcmus-private/            # Private submodule (credentials, piracy workflows)
├── ielts/, toeic/            # English test prep (storage only)
├── general/                  # Misc documents (storage only)
├── thikhoinghiem2026/        # ARCHIVED — SV_STARTUP, did not advance
├── events/, personal/, tmp/  # Non-code directories
```

Each course repo uses `extracted_content/` for markdown extracted from PPSX/PDF slides.

## Course Details

**intro-oop1/ — OOP1 (C++ Programming)**
- C++14 strict (teacher requirement). Must load into Visual Studio before submission.
- Homework: `MSSV_______.cpp`. Final project: Caro game (raylib). Docs: `DoAnCaro.pdf`
- Slides: PPSX in `baigiang/`, extracted to `extracted_content/`

**science-socialism/** — Has own `CLAUDE.md` with chapter boundaries and grading structure.

## Moodle (courses.hcmus.edu.vn)

Auth: Microsoft 365 OAuth. Bulk download workflow in `hcmus-private/CLAUDE.md`.

| Course | ID | Workspace |
|---|---|---|
| OOP1 | 16047 | `semester2/intro-oop1/` |
| Nhập môn KHGD | 16048 | `semester2/intro-edu-science/` |
| Xác suất thống kê (MTH00044) | 15966 | `semester2/probability-statistics/` |
| Lịch sử Đảng CSVN | 16150 | `semester2/history-vcp/` |
| CNXH khoa học | 16128 | `semester2/science-socialism/` |

## PPSX/PPTX Extraction

PPSX = ZIP. No python-pptx/LibreOffice needed:
- Text: `unzip -p file.ppsx ppt/slides/slideN.xml` → parse `<a:t>` tags
- Images: `unzip -j file.ppsx "ppt/media/*" -d out/`
- Mapping: `ppt/slides/_rels/slideN.xml.rels` → `Target="../media/imageX.png"`
- Output: Markdown with `## Slide N` sections, code blocks, Mermaid for diagrams

## PDF Textbook Extraction

For extracting textbook chapters from PDF to markdown (e.g., Ron Larson's Elementary Statistics):

### Step 1: Extract raw text with PyMuPDF
```bash
cd <course-dir>
uv venv && uv pip install pymupdf
.venv/bin/python3 -c "
import fitz
doc = fitz.open('path/to/textbook.pdf')
for i in range(START_PAGE, END_PAGE):
    page = doc[i]
    text = page.get_text()
    book_page = i - OFFSET  # adjust for front matter
    print(f'=== PDF PAGE {i+1} (BOOK PAGE {book_page}) ===')
    print(text)
" > extracted_content/chapterN/raw_text.txt
```

### Step 2: Claude fixes math formulas (hybrid approach)
- PyMuPDF loses math formulas (rendered as vector graphics/special fonts in PDFs)
- After raw extraction, Claude reads the PDF visually **2-3 pages at a time** to fix garbled math
- Math formulas → LaTeX notation (`$x^2$`, `$$\sum_{i=1}^{n}$$`)
- This avoids installing heavy ML tools (marker/nougat need 3-6 GB RAM + GPU)

### Step 3: Spawn parallel sub-agents to write markdown
- One agent per subchapter/file — if one gets blocked by content filtering, others still complete
- Each agent reads `raw_text.txt` and writes its assigned markdown file
- For math-heavy chapters: agent also reads relevant PDF pages visually to fix formulas
- Use `model: "sonnet"`, `run_in_background: true` for all agents
- Include a `README.md` with TOC table linking all files

### Output format
- One markdown file per section: `N.M-section-name.md`
- Definitions as blockquotes (`> **Definition:** ...`)
- Math formulas in LaTeX: inline `$...$`, display `$$...$$`
- Examples with solutions, Try It Yourself exercises
- Full exercise sets preserved
- Tables for data, text descriptions for diagrams/figures
- `README.md` with TOC table (File | Section | Topic | Pages)

### Why this hybrid approach?
- **PyMuPDF alone**: loses math formulas (garbled text)
- **Claude PDF reader alone**: dumps page images (wastes context), content filtering blocks large outputs
- **marker/nougat**: need 3-6 GB RAM + GPU, slow on CPU-only servers
- **Hybrid (PyMuPDF + Claude visual fix)**: reliable, no extra dependencies, handles math correctly

## Exercise Solving Rules

When solving any exercise from textbooks (especially probability-statistics):
- **ALWAYS verify results with Python** (numpy, scipy, pandas) after solving
- Write a Python script that computes the answer independently
- Compare manual/analytical solution against Python output
- Flag any discrepancies before presenting the answer
- This applies to ALL exercises: examples, Try It Yourself, section exercises, review, quiz

## YouTrack

Project **FISHcmus** (key: `FIS`). Track all university tasks, assignments, and deadlines here.

## Conventions

- Always check subdirectory `CLAUDE.md` before working in a course area
- MATLAB naming: `baitap_ngay<DD>_thang<MM>_<YYYY>.m`
- Private/sensitive data in `hcmus-private/` submodule (always private on GitHub)
