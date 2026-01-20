

### 1. Toggle Button Behavior

**Question:** For the new brightness/contrast adjustment toggle button, should clicking on the OCT image behave as follows?

| Toggle State | Left-Click Drag Behavior |
|--------------|-------------------------|
| **OFF (default)** | Pan the image |
| **ON (checked)** | Adjust brightness (vertical drag) / contrast (horizontal drag) |

The toggle button will be placed **to the left of** the existing "Save brightness/contrast" and "Reset brightness/contrast" buttons, and will use the existing `imageAdjustments.png` icon.

**Please confirm:** Is this the expected behavior, or should something be different?

---

### 2. Mode Interactions

**Question:** Should the following mode interactions be implemented?

| Scenario | Behavior |
|----------|----------|
| User enables **Brightness/Contrast** mode while **Measure** mode is active | Measure mode is automatically disabled |
| User enables **Measure** mode while **Brightness/Contrast** mode is active | Brightness/Contrast mode is automatically disabled |
| User enters **Layer Edit** mode (segmentation editing) | Brightness/Contrast mode is automatically disabled |
| User navigates to a **different image** | Brightness/Contrast mode is reset to OFF |

**Please confirm:** Are these mutual exclusivity rules correct, or should multiple modes be allowed simultaneously?