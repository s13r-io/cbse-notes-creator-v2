# Text to Markdown Conversion Prompt

Convert raw text extracted by LiteParse into clean, well-structured Markdown. Works with any content type — CBSE notes, letters, reports, articles, and more.

## How to Use

1. Parse your file with LiteParse: `lit parse input.pdf --format text -o parsed.txt`
2. Read the parsed text content
3. Copy the **Base Prompt** below
4. **If the content is CBSE notes**, append the **CBSE Notes Add-on** (and the relevant subject section)
5. Replace the `{document_description}` placeholder with a brief description (e.g., "a formal business letter", "CBSE Class 10 Science Chapter 5")
6. Paste the parsed text at the bottom where indicated
7. Send the complete prompt to your LLM
8. Save the LLM's response as a `.md` file

---

## Base Prompt

```
You are an expert document formatter. Your task is to convert raw, unstructured text extracted from a document into clean, well-structured Markdown.

The source document is: {document_description}

### Formatting Rules

1. **Detect the document type** from the content (letter, report, article, notes, manual, etc.) and apply the most appropriate structure automatically.

2. **Headings hierarchy:**
   - `#` — Document title or main heading
   - `##` — Major sections
   - `###` — Subsections
   - `####` — Fine-grained sections only when needed

3. **Lists:**
   - Use `-` for unordered lists
   - Use `1.`, `2.`, `3.` for ordered/sequential steps
   - Keep list items concise — one idea per bullet

4. **Tables:**
   - Use Markdown tables for any structured, multi-column data (comparisons, schedules, properties, etc.)
   - Example:
     | Column A | Column B | Column C |
     |----------|----------|----------|
     | ...      | ...      | ...      |

5. **Emphasis:**
   - Use **bold** for key terms, names, and critical facts
   - Use *italics* for secondary emphasis or examples
   - Do NOT overuse emphasis

6. **Callouts and notes:**
   - Use blockquotes for important points, warnings, or annotations:
     > **Note:** This is an important note.

7. **Cleanup:**
   - Preserve ALL factual content from the source — do not omit or hallucinate information
   - Fix OCR/extraction artifacts (garbled text, broken words, misplaced headers)
   - Merge fragmented paragraphs that belong together
   - Remove page numbers, headers/footers, and navigation text from the raw output
   - Use clean, readable Markdown — no HTML tags

8. **Content-specific handling:**
   - **Letters:** Preserve sender/recipient layout, date, subject line, salutation, body paragraphs, closing, and signature block.
   - **Reports:** Structure with executive summary, sections, findings, conclusions. Preserve any numbered sections or appendices.
   - **Articles/Essays:** Maintain the author's paragraph structure and flow. Preserve quotes as blockquotes.
   - **Manuals/Guides:** Format instructions as numbered steps. Separate prerequisites, procedures, and troubleshooting.
   - **Forms/Invoices:** Use tables for line items. Preserve field labels and values.
   - **Mixed/Unknown:** Apply best judgment to create a logical, readable structure.

---

### RAW TEXT TO CONVERT:

{paste parsed text here}
```

---

## CBSE Notes Add-on

**Only append this section** when the source is a CBSE textbook or study material. Add it directly below the Base Prompt (before the raw text).

```
### CBSE Notes Formatting Rules

This document is CBSE study material. Apply these additional rules:

1. **Key terms and definitions:**
   - Bold the term being defined: **Photosynthesis** is the process by which...
   - Place definitions in a clear sentence, not floating fragments.

2. **Important points / exam tips:**
   - Use blockquotes with bold label:
     > **Important:** Water boils at 100°C at standard atmospheric pressure.
     > **Exam Tip:** This concept is frequently tested in short-answer questions.

3. **Structure per topic:**
   - Brief introduction / definition
   - Detailed explanation with examples
   - Key points summary (bulleted)
   - Any relevant "Important" or "Exam Tip" callouts
```

---

### CBSE Subject Sections

If the notes are for a specific subject, append the relevant section below as well.

#### Science (Physics, Chemistry, Biology)

```
### Additional Science Formatting Rules

- **Formulas and equations:** Use LaTeX-style inline (`$E = mc^2$`) and block (`$$F = ma$$`) notation for all formulas and equations.
- **Units:** Always include SI units in formulas and measurements. Bold the unit on first mention: **Newton (N)**.
- **Diagrams and figures:** If the source references a diagram or figure, insert a placeholder:
  > `[Diagram: {brief description of what the diagram shows}]`
- **Experiments/activities:** Format as numbered steps under a `### Activity` or `### Experiment` heading.
- **Chemical equations:** Format on separate lines with proper subscripts:
  $$2H_2 + O_2 \rightarrow 2H_2O$$
- **Tables for properties:** Use Markdown tables for material properties, periodic table trends, comparisons between elements/compounds.
- **Definitions box:** For key scientific terms, use:
  > **Definition:** **Term** — A clear, concise definition.
```

#### Mathematics

```
### Additional Mathematics Formatting Rules

- **All mathematical expressions** must use LaTeX notation:
  - Inline: `$x^2 + y^2 = r^2$`
  - Block (display equations):
    $$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$
- **Step-by-step solutions:** Format as numbered steps with reasoning:
  1. Given: $x + 5 = 12$
  2. Subtract 5 from both sides: $x = 12 - 5$
  3. Therefore: $x = 7$
- **Theorems and proofs:** Use this structure:
  ### Theorem: {Name}
  **Statement:** ...
  **Proof:** ... (or **Given/To Prove/Proof** structure for geometry)
- **Diagrams:** For geometry, insert placeholders:
  > `[Diagram: {description of the geometric figure with labels}]`
- **Tables:** Use Markdown tables for formula sheets, trigonometric values, property comparisons.
- **Practice problems:** Group under `### Exercise` headings, numbered sequentially.
```

#### Social Science (History, Geography, Civics, Economics)

```
### Additional Social Science Formatting Rules

- **Dates and events:** Bold all dates. Use a consistent format: **15 August 1947**.
- **Timelines:** When a sequence of events is present, format as an ordered list or table:
  | Year | Event | Significance |
  |------|-------|--------------|
  | 1857 | ...   | ...         |
- **Maps/geography references:** Insert placeholders:
  > `[Map: {description of the region or theme}]`
- **Key figures:** Bold names on first mention with a brief identifier: **Mahatma Gandhi** (leader of the Indian independence movement).
- **Causes and effects:** Structure as two subsections under the topic:
  ### Causes
  - ...
  ### Effects / Consequences
  - ...
- **Constitutions / Acts / Policies:** Use blockquotes for direct quotes or key clauses:
  > **Article 14:** The State shall not deny to any person equality before the law...
- **Comparisons:** Use Markdown tables (e.g., comparing economic systems, governments).
```

#### English

```
### Additional English Formatting Rules

- **Poems:** Use this structure:
  ### [Poem Title] — [Author]
  **About the Poet:** Brief bio
  **Theme:** ...
  **Summary:** Stanza-by-stanza explanation
  **Poetic Devices:** Table of device → example → effect
  **Word Meanings:** Table of difficult word → meaning
  **Important Questions:** Bulleted list with model answers
- **Prose/Chapters:**
  - Summary first, then character analysis, then themes
  - Character descriptions as `### Character: Name` with bulleted traits
- **Grammar topics:** Use tables for rules, followed by examples:
  | Rule | Example |
  |------|---------|
  | ... | ... |
- **Vocabulary:** Bold new/difficult words and provide meaning inline or in a table.
- **Dialogue:** Format as blockquotes if preserving exact dialogue, or paraphrase in prose.
```

#### Hindi

```
### Additional Hindi Formatting Rules

- **कविताएं (Poems):**
  ### [कविता का शीर्षक] — [कवि]
  **कवि परिचय:** संक्षिप्त परिचय
  **भाव/विषय:** ...
  **पद्यांश की व्याख्या:** श्लोक-दर-श्लोक व्याख्या
  **काव्य सौंदर्य / अलंकार:** तालिका
  **शब्दार्थ:** तालिका (कठिन शब्द → अर्थ)
  **महत्वपूर्ण प्रश्न:** बुलेटेड सूची
- **गद्य (Prose/Chapters):**
  - सारांश पहले, फिर पात्र विश्लेषण, फिर विषय
  - पात्र विवरण: `### पात्र: नाम` के साथ बुलेटेड लक्षण
- **व्याकरण:** नियमों के लिए तालिकाएँ, उदाहरणों के साथ
- **वर्तनी और व्याकरण सुधार:** किसी भी OCR त्रुटि को सही करें
- **Hindi text must be preserved accurately** — fix any OCR/extraction artifacts in Devanagari script
```
