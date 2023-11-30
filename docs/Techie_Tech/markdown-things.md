---
tags:
    - Markdown
    - LaTeX
---
# Some Markdown Things

These things are specific to this repo, i.e., markdown using `mkdocs-material`. There are additional changes in `extra.css` which enables these features.  
**NOTE :** These may not work with other markdown editors.

## 1. Note Referencing

- While referencing a note whose name is not unique, like `index.md` use `[<name>](<relative path> like ../Definitions/index#subsection)`
- In other cases, directly use `[[<name_of_file>#subsection | <name>]]`.

## 2. Image Aligning and Resizing

- Use `{: style="height:150px;width:150px"}` after the image link. For example, `![](){: style="height:10cm;width:15cm"}` or `![](){: style="height:90%;width:90%`.
- For center aligning, use `{: .center}` after the image link. For example, `![](){: .center style="height:100%;width:100%"}`.

## 3. Spacing in Math Mode (LaTeX)

In increasing order of spacing, use 

- \\: 
- \\;
- \\
- \quad
- \qquad
