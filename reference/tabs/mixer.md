# Mixer Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Displays Audio Mixer exposed parameters and group volume levels. Provides a setup guide for connecting an Audio Mixer to the tab.

---

## Setup

The Mixer tab requires an `AudioMixer` asset with at least one exposed parameter.

To set up:

1. Open the Audio Mixer in Unity (`Window > Audio > Audio Mixer`).
2. Right-click a parameter and select **Expose Parameter**.
3. Give the exposed parameter a name.
4. In the Runtime Atlas Mixer tab, click **Auto-Configure** or manually assign the mixer asset.

See [Audio Mixer Setup](../../guides/audio-mixer-setup.md) for step-by-step instructions.

---

## Display

Once configured, the Mixer tab shows:

| Column | Description |
|--------|-------------|
| Parameter name | Exposed parameter label |
| Value | Current parameter value (editable) |
| Slider | Visual slider matching the parameter range |

Changes made to parameter values in the Mixer tab take effect immediately on the live `AudioMixer`.

---

## Setup Step Indicator

When no mixer is configured, the tab shows a numbered setup guide:

1. Open the Audio Mixer in Unity
2. Expose at least one parameter
3. Assign the mixer in the Runtime Atlas settings or use Auto-Configure

Each step is highlighted green when completed.
