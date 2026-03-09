# CLAUDE.md

Academic workspace for Nguyen Huu Thien Nhan (nhannht), HCMUS Education Technology program.

## Student Info

- **Student ID:** 25310023
- **Git:** `nhannht` / `nhanclassroom@gmail.com` / https://github.com/nhannht

## Directory Structure

```
hcmus/
├── fishcmus_github/          # Quartz site → fishcmus.github.io (semester 1)
├── semester2/                # Semester 2 (2025-2026) active workspaces
│   ├── intro-oop1/           # OOP1 — C++14, raylib Caro project
│   └── science-socialism/    # CNXHKH — has own CLAUDE.md
├── semester%201/              # Legacy (URL-encoded space)
├── ielts/, toeic/            # English test prep (storage only)
├── general/                  # Misc documents (storage only)
├── thikhoinghiem2026/        # ARCHIVED — SV_STARTUP, did not advance
├── events/, personal/, tmp/  # Non-code directories
```

## fishcmus_github

Quartz v4 static site for semester 1 coursework. Obsidian-flavored Markdown, Git LFS for PDFs.

```bash
cd fishcmus_github && npm ci && npx quartz build   # or: npx quartz serve
```

- **Branch:** master (not main). Auto-deploys via GitHub Actions on push.
- **Config:** `quartz.config.ts`, `quartz.layout.ts`, `.github/workflows/build_doc.yml`
- **Landing page:** `profile/README.md` (symlinked as index.md)
- **Course dirs** (`semester-1/`): `baigiang/`, `dethi/`, `thuchanh/`, PDFs, per-course `CLAUDE.md`
- **Courses:** calculus-1 (MTH00021, has MATLAB+Python), linear-algebra, general-chemistry-1, intro-edtech, intro-marxism-leninism, marxism-economic

## semester2/ (Active)

Semester 2 workspaces live directly under `semester2/`, not inside fishcmus_github.

**intro-oop1/ — OOP1 (C++ Programming)**
- C++14 strict (teacher requirement). Must load into Visual Studio before submission.
- Homework: `MSSV_______.cpp`. Final project: Caro game (raylib). Docs: `DoAnCaro.pdf`
- Slides: PPSX in `baigiang/`, extracted to `baigiang/markdown/`

**science-socialism/** — Has own `CLAUDE.md` with chapter boundaries and grading structure.

## Moodle (courses.hcmus.edu.vn)

Auth: Microsoft 365 OAuth. Bulk download: browsermcp → scrape IDs → decrypt Edge cookie → `curl -b`. See `~/nhannht-admin/docs/hacking/chromium-cookie-decryption.md`.

| Course | ID | Workspace |
|---|---|---|
| OOP1 | 16047 | `semester2/intro-oop1/` |
| Nhập môn KHGD | 16048 | — |
| Xác suất thống kê (MTH00044) | 15966 | — |
| Lịch sử Đảng CSVN | 16150 | — |
| CNXH khoa học | 16128 | `semester2/science-socialism/` |

## PPSX/PPTX Extraction

PPSX = ZIP. No python-pptx/LibreOffice needed:
- Text: `unzip -p file.ppsx ppt/slides/slideN.xml` → parse `<a:t>` tags
- Images: `unzip -j file.ppsx "ppt/media/*" -d out/`
- Mapping: `ppt/slides/_rels/slideN.xml.rels` → `Target="../media/imageX.png"`
- Output: Markdown with `## Slide N` sections, code blocks, Mermaid for diagrams

## YouTrack

Project **FISHcmus** (key: `FIS`). Track all university tasks, assignments, and deadlines here.

## Conventions

- Always check subdirectory `CLAUDE.md` before working in a course area
- MATLAB naming: `baitap_ngay<DD>_thang<MM>_<YYYY>.m`
- Private/sensitive data never in version control
