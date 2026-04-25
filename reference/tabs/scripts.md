# Scripts Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Displays the source code of any script file in the project. Used to review code directly within the Runtime Atlas window, typically navigated to from Scanner or Optimizer results.

---

## Opening a Script

Scripts are opened in this tab by:

- Clicking **Open** on a Scanner result row
- Clicking **Open** on an Optimizer suggestion card
- Navigating via `Window > Runtime Atlas > Tabs > Inspector` (which activates the Scripts viewer inside the Inspector tab workflow)

---

## Display

The viewer renders source code with line numbers. The view scrolls to the flagged line automatically when opened from a Scanner or Optimizer result.

### Features

| Feature | Description |
|---------|-------------|
| **Line numbers** | Displayed in the gutter |
| **Scroll-to-line** | Automatically scrolls to the target line on open |
| **Virtualized rendering** | Only visible lines are drawn — large files do not cause performance issues |
| **Read-only** | The viewer is display-only; editing is not supported |

---

## Limitations

- Syntax highlighting is not applied. Source is displayed as plain text.
- Binary or non-UTF-8 files are not supported.
- Only files within the Unity `Assets/` directory can be opened.
