---
name: latex-chinese-summary
description: >
  Generates a Chinese summary of a LaTeX document (`main.tex`) by filling in
  `template.tex` in the same folder. Trigger this skill whenever the user says
  anything like "make a summary for main.tex", "summarize main.tex in Chinese",
  "fill in the template", or any variant that involves summarizing a LaTeX paper
  into a Chinese-language template. The skill reads both files, writes the
  completed summary into template.tex, and never touches main.tex or any other
  file. Always use this skill for LaTeX Chinese summary tasks — do not attempt
  this workflow without it.
---

# LaTeX Chinese Summary Skill

Generate a Chinese-language summary of `main.tex` by completing `template.tex`
in the same directory. This is the only file you are allowed to modify.

---

## Workflow

### 1. Locate the files

Both files must exist in the same directory. The user usually runs this from
that directory, so the paths are:

```
main.tex
template.tex
```

If either file is missing, tell the user and stop.

### 2. Read `main.tex` thoroughly

Parse and understand:

- **Title and abstract** – translate the abstract in full to Chinese. Do **not** extract or include author names, affiliations, or contact information.
- **Section structure** – introduction, methods, experiments/results,
  conclusion, and any other named sections.
- **All figures** – for every `\begin{figure}...\end{figure}` block capture:
  - The caption text (`\caption{...}`)
  - The label (`\label{...}`)
  - The image filename (`\includegraphics{...}`)
  - What the figure likely depicts (infer from caption + surrounding text)
- **Tables** – note key data or findings presented in tables.
- **Key results and conclusions** – numbers, trends, comparisons that matter.

### 3. Read `template.tex`

Identify every placeholder. Common patterns include but are not limited to:

```
[summary here]   {{content}}   % TODO   PLACEHOLDER   ______
```

Also note any structural commands the template enforces
(`\section{}`, `\textbf{}`, `\begin{itemize}`, custom macros, etc.)
that must be preserved exactly.

### 4. Write the completed `template.tex`

Rules:
- **Only edit `template.tex`** – never touch `main.tex` or any other file.
- Preserve every LaTeX formatting command from the original template.
- Replace every placeholder with Chinese summary content derived from `main.tex`.
- Write all summary prose **in Chinese (简体中文)**.
- **Do NOT include author names, affiliations, emails, or any author metadata** – even if present in `main.tex` or in a template placeholder. Leave author-related placeholders blank or remove them entirely.

Content to include (map to whichever template sections exist):

| Content | Guidance |
|---|---|
| 摘要 (Abstract) | Full Chinese translation of the original abstract |
| 研究目的 | What question/problem the paper addresses |
| 方法 | Key methods, models, datasets, experimental setup |
| 主要结果 | Important findings; cite figure labels where relevant (e.g., 如图~\ref{fig:xxx}所示) |
| 图表说明 | For each significant figure: what it shows and what insight it provides |
| 结论 | Main takeaways and implications |

Keep the summary concise — 1–2 pages of compiled output unless the template
specifies otherwise.

### 5. Verify before saving

Before writing, mentally check:
- [ ] No placeholder text remains in `template.tex`.
- [ ] All LaTeX commands from the original template are intact.
- [ ] `main.tex` is untouched.
- [ ] All prose is in Chinese.
- [ ] At least one figure is mentioned (if figures exist in `main.tex`).

Then write the completed content to `template.tex`.

### 6. Report to the user

After saving, confirm:
- What was summarized (paper title / topic).
- Which sections were filled.
- How many figures were incorporated.
- That `main.tex` was not modified.

---

## Edge Cases

| Situation | Action |
|---|---|
| `template.tex` has no visible placeholders | Fill in template sections with Chinese summary content using the template's existing structure as a guide |
| Template has an author/affiliation placeholder | Leave it blank or delete the placeholder — do not fill in any author information |
| `main.tex` has no figures | Skip figure discussion; note this to the user |
| Template is in English | Keep all structural English commands; write only the prose content in Chinese |
| Abstract is very long | Summarize faithfully but trim redundant sentences; still translate the core claims fully |
| Multiple figure files referenced | Describe each one briefly; group related figures if the template space is limited |

---

## Example placeholder replacements

**Template line:**
```latex
\section{摘要}
[abstract translation here]
```

**After filling:**
```latex
\section{摘要}
本文研究了……（完整中文翻译）
```

**Template line:**
```latex
\textbf{主要结果：} {{results}}
```

**After filling:**
```latex
\textbf{主要结果：} 实验表明，所提方法在……数据集上达到了……，如图~\ref{fig:result}所示。
```
