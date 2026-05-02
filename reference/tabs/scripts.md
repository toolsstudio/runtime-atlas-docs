# Scripts Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Displays the source code of any `.cs` file in the project. Used to review code in context after navigating from a Scanner result or Optimizer suggestion.

---

## Opening a Script

Scripts are opened from:

- **Scanner** tab — clicking **Open** on a result row
- **Optimizer** tab — clicking **Open** on a suggestion card
- **Console** tab — clicking a log entry that has source file information
- Drag-and-drop — dragging a `.cs` file from the Project window onto the drop zone at the top of the Scripts tab

---

## Drop Zone

A drop target is rendered at the top of the tab. Drag any `.cs` file from the Project window onto it to open that file. Only `.cs` files are accepted.

---

## Viewer Features

| Feature | Description |
|---------|-------------|
| **Line numbers** | Displayed in the left gutter |
| **Scroll-to-line** | Scrolls automatically to the target line when opened from a result |
| **Virtualised rendering** | Only visible lines are drawn. Large files do not cause frame time spikes. |
| **Read-only** | Display only. Editing is not supported. |
| **Open in IDE** | Opens the current file at the current line in the external script editor configured in Unity Preferences |

---

## Limitations

- No syntax highlighting. Source is displayed as plain text with line numbers.
- Binary or non-UTF-8 files are not supported and will not render correctly.
- Only files within the Unity `Assets/` directory can be opened.
