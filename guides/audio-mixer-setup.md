# Audio Mixer Setup
**Runtime Atlas v1.2.0**

---

## Overview

The Mixer tab requires an `AudioMixer` asset with at least one exposed parameter. This guide walks through exposing parameters and connecting the mixer to Runtime Atlas.

---

## Step 1 — Create or Locate Your Audio Mixer

If you do not already have an Audio Mixer:

1. In the Project window: `Assets > Create > Audio Mixer`.
2. Name it (e.g., `MainMixer`).
3. Open it: `Window > Audio > Audio Mixer`.

---

## Step 2 — Expose Parameters

In the Audio Mixer window:

1. Select a group (e.g., `Master`).
2. In the Inspector, right-click the **Volume** property.
3. Select **Expose '...' to script**.
4. In the **Exposed Parameters** panel (top-right of the mixer window), rename the parameter to a descriptive label (e.g., `MasterVolume`).

Repeat for any parameters you want visible in the Runtime Atlas Mixer tab.

---

## Step 3 — Connect to Runtime Atlas

### Option A — Auto-Configure

In the Runtime Atlas Mixer tab, click **Auto-Configure**. Runtime Atlas scans the project for `AudioMixer` assets and selects the first one it finds. If your project has multiple mixers, use Option B for precision.

### Option B — Manual Assignment

1. Open **Edit > Project Settings > Runtime Atlas**.
2. In the **Mixer** section, drag your `AudioMixer` asset into the **Audio Mixer** field.

---

## Step 4 — Verify

1. Enter Play Mode.
2. Open the **Mixer** tab.
3. Confirm exposed parameters appear in the list with editable values.

---

## Notes

- Only exposed parameters are shown. Non-exposed parameters (Volume, Pitch, etc.) that have not been explicitly exposed via the right-click menu are not visible in the Mixer tab.
- Parameter value ranges are defined by the parameter type in the mixer. Volume parameters are typically in the range [-80, 0] dB.
- Changes made in the Mixer tab call `audioMixer.SetFloat(paramName, value)` immediately and affect the live mixer in Play Mode.
