# Optimizer Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Converts Script Scanner results into structured, actionable suggestions. Each suggestion identifies the issue, explains why it matters, and provides concrete resolution steps.

---

## Workflow

1. Run a scan in the **Scanner** tab.
2. Open the **Optimizer** tab. Suggestions populate automatically from the scan results.
3. Review each suggestion card.
4. Click **Open** to navigate to the flagged line in the Scripts viewer.

If no scan has been run, the tab prompts to run the Scanner first.

---

## Suggestion Card Fields

| Field | Description |
|-------|-------------|
| **Title** | Short name of the issue pattern |
| **Severity** | Info, Warning, or Critical |
| **Detail** | Explanation of why this pattern is a problem |
| **How to Fix** | Concrete resolution steps |
| **File** | Script file path |
| **Line** | Line number |
| **Open** | Opens the Scripts viewer at that line |

---

## Suggestion Count

The tab shows the total suggestion count after a scan. Zero means no actionable items were produced from the current scan.

---

## Relationship to Scanner

Suggestions are derived exclusively from the most recent Scanner scan results. The Optimizer has no independent scan logic. Re-running the Scanner always refreshes the Optimizer.
