# Scripts Tab
**Runtime Atlas v1.2.0**

---

## Purpose

A read-only source file viewer with line number navigation. Opens files from within the editor without switching to an external IDE.

---

## Opening a File

Files can be opened in the Scripts tab from:

- Clicking a file path in the Scanner results list
- Directly, via the file browser in the Scripts tab itself

---

## Navigation

| Control | Action |
|---------|--------|
| Line number field | Type a line number and press Enter to jump to it |
| Scroll | Mouse wheel or drag the scroll bar |
| File browser | Click the folder icon to open a different file |

---

## Display

The file is rendered as virtualized visible lines — only lines currently in the scroll viewport are drawn. This allows large files (10,000+ lines) to be scrolled without editor lag.

Lines are displayed with line numbers. No syntax highlighting is applied.

---

## Limitations

The Scripts tab is read-only. Editing requires opening the file in the IDE (double-clicking the file in the Project window).
