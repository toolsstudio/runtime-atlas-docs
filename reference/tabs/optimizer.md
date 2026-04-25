# Optimizer Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Converts Script Scanner results into structured, actionable suggestions. Each suggestion explains what the issue is, why it matters, and how to resolve it.

---

## Workflow

The Optimizer tab requires a completed Scanner scan. If no scan has been run, the tab displays a prompt to run the scanner first.

After a scan:

1. Open the **Optimizer** tab.
2. Suggestions are displayed automatically — no additional action needed.
3. Each suggestion card shows the issue, severity, affected file and line, and resolution steps.
4. Click **Open** to navigate to the flagged line in the Scripts viewer.

---

## Suggestion Card Fields

| Field | Description |
|-------|-------------|
| **Title** | Short name of the issue pattern |
| **Severity** | Info, Warning, or Critical |
| **Detail** | Explanation of why the pattern is a problem |
| **How to Fix** | Concrete resolution steps |
| **File** | Script file path |
| **Line** | Line number |
| **Open** | Opens the Scripts viewer at that line |

---

## Suggestion Count

The tab header shows the total suggestion count after a scan. A count of zero means no actionable items were found from the current scan results.

---

## Relationship to Scanner

Suggestions are derived exclusively from the most recent Scanner scan. Re-running the Scanner refreshes the Optimizer automatically.
