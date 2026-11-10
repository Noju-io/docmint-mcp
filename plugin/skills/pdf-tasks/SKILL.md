---
name: pdf-tasks
description: Work on PDF and image files with Docmint. Use when the user wants to compress a PDF or get it under a size limit, merge or combine PDFs, split a PDF or extract pages, delete, reorder or rotate pages, add page numbers or a watermark, crop or resize pages, make a scan searchable (OCR), extract text, convert PDF pages to JPG or PNG, turn photos or images into a PDF, sign a PDF, add or remove a password, flatten forms, edit metadata, compare two PDFs, inspect a PDF, or compress, resize or convert images (including HEIC to JPG).
---

# PDF and image tasks with Docmint

Docmint has two sets of tools. Use whichever is available in this session.

## Local tools (Claude Code, and Cowork on the user's computer)

The `docmint` server runs on the user's machine and works on files directly. Tool names end in `_pdf` or describe the action, such as `compress_pdf`, `merge_pdf`, `split_pdf`, `ocr_pdf`, `sign_pdf`, `images_to_pdf`, `process_image`.

1. Pass each file as a local path. Use base64 only when you cannot give a path.
2. Results are written next to the input file unless you set `output_dir` or `output_path`. Tell the user the path of each file written.
3. For a size target ("under 2 MB"), run `compress_pdf` with a level, check the size in the result, and try a stronger level once if it is still too large. Say so if the target can't be reached.
4. Page ranges use 1-based pages, such as `1-3,5`.
5. Run `inspect_pdf` first when you need the page count, encryption status or page sizes before choosing settings.
6. If a call fails because the daily free runs are used up, tell the user and offer `connect_docmint_account`, which links their Docmint account. Don't retry in a loop.

## Link tools (claude.ai chat, or when the local tools are missing)

The `docmint-links` connector does not receive files. It finds the right Docmint tool and returns a link with the settings filled in; the user opens it, adds the file, and it is processed in their browser without being uploaded.

1. Call `find_pdf_tool` with the task in the user's words.
2. Call `get_tool_link` with the best match's id and any settings the user asked for, such as `level=strong` for compress-pdf or `mode=range` and `ranges=1-3` for split-pdf. `list_pdf_tools` lists each tool's settings.
3. Give the user the link with one sentence saying what it will do. Mention any settings the result says it ignored.

## Both

- Don't claim a file was changed until a local tool's result confirms it.
- Keep the original file. Docmint writes new files rather than overwriting.
- Passwords the user gives for `protect_pdf` or `unlock_pdf` go only into that tool call. Don't repeat them in the reply.
