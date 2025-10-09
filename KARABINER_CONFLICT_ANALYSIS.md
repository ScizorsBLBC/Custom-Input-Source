# Karabiner Elements & HiraganaLaser Conflict Analysis

## **Issue Summary**

When using the HiraganaLaser input source, Karabiner Elements remappings for the F1-F12 row and navigation cluster keys (above arrow keys) output the Hiragana characters instead of their intended remapped functions. The remappings work correctly when using the ABC English input source.

## **Root Cause Analysis**

### **Karabiner Elements Configuration Overview**

Your Karabiner Elements setup includes:

1. **F1-F12 Key Mappings**:
   - F1 → ` (grave_accent_and_tilde)
   - F2 → 1
   - F3 → 2
   - F4 → 3
   - F5 → 4
   - F6 → 5
   - F7 → 6
   - F8 → 7
   - F9 → 8
   - F10 → 9
   - F11 → 0
   - F12 → \ (backslash)

2. **F1-F12 Shift Mappings**:
   - Shift+F1 → ~ (shifted grave)
   - Shift+F2 → ! (shifted 1)
   - Shift+F3 → @ (shifted 2)
   - Shift+F4 → # (shifted 3)
   - Shift+F5 → $ (shifted 4)
   - Shift+F6 → % (shifted 5)
   - Shift+F7 → ^ (shifted 6)
   - Shift+F8 → & (shifted 7)
   - Shift+F9 → * (shifted 8)
   - Shift+F10 → ( (shifted 9)
   - Shift+F11 → ) (shifted 0)
   - Shift+F12 → | (shifted backslash)

3. **Navigation Cluster Mappings**:
   - Print Screen → - (hyphen)
   - Scroll Lock → = (equal_sign)
   - Pause → [ (open_bracket)
   - Insert → ; (semicolon)
   - Home → ' (quote)
   - Page Up → ] (close_bracket)
   - Delete Forward → , (comma)
   - End → . (period)
   - Page Down → / (slash)

### **Conflict Points with HiraganaLaser Layout**

The conflict occurs because:

1. **Key Code Translation Order**:
   ```
   Physical Key → Karabiner Elements → HiraganaLaser Layout → Application
   ```

2. **HiraganaLaser Layout Intercepts Remapped Keys**:
   - When Karabiner remaps F1 to ` (grave_accent_and_tilde), the HiraganaLaser layout sees this as key code 50
   - Key code 50 in HiraganaLaser maps to ろ (ro)
   - The layout processes the remapped key code and outputs ろ instead of the intended `

3. **Specific Conflict Mappings**:

| Karabiner Remap | Key Code | HiraganaLaser Output | Intended Output |
|-----------------|----------|---------------------|-----------------|
| F1 → ` | 50 | ろ (ro) | ` |
| F2 → 1 | 18 | ぬ (nu) | 1 |
| F3 → 2 | 19 | ふ (fu) | 2 |
| F4 → 3 | 20 | あ (a) | 3 |
| F5 → 4 | 21 | う (u) | 4 |
| F6 → 5 | 23 | え (e) | 5 |
| F7 → 6 | 22 | お (o) | 6 |
| F8 → 7 | 26 | や (ya) | 7 |
| F9 → 8 | 28 | ゆ (yu) | 8 |
| F10 → 9 | 25 | よ (yo) | 9 |
| F11 → 0 | 29 | わ (wa) | 0 |
| F12 → \ | 42 | む (mu) | \ |

## **Why It Works with ABC English Input Source**

The ABC English input source doesn't have custom key mappings, so:
1. Karabiner Elements remaps the keys
2. ABC input source passes through the remapped key codes unchanged
3. Applications receive the intended characters

## **Potential Solutions**

### **Solution 1: Input Source Conditional Rules (Recommended)**

Modify Karabiner Elements rules to only apply when NOT using HiraganaLaser input source:

```json
{
  "description": "F1-F12 keycap character mappings (ABC only)",
  "manipulators": [
    {
      "from": { "key_code": "f1" },
      "to": [{ "key_code": "grave_accent_and_tilde" }],
      "type": "basic",
      "conditions": [
        {
          "type": "input_source_if",
          "input_sources": [
            {
              "input_source_id": "com.apple.keylayout.ABC"
            }
          ]
        }
      ]
    }
  ]
}
```

### **Solution 2: Device-Specific Rules**

Apply Karabiner rules only to specific devices (excluding the DAS Keyboard 4 Pro):

```json
{
  "description": "F1-F12 keycap character mappings (Internal keyboard only)",
  "manipulators": [
    {
      "from": { "key_code": "f1" },
      "to": [{ "key_code": "grave_accent_and_tilde" }],
      "type": "basic",
      "conditions": [
        {
          "type": "device_if",
          "identifiers": [
            {
              "is_keyboard": true,
              "product_id": 65278,
              "vendor_id": 3141
            }
          ]
        }
      ]
    }
  ]
}
```

### **Solution 3: HiraganaLaser Layout Modification**

Modify the HiraganaLaser layout to exclude the conflicting key codes, but this would break the Hiragana functionality.

### **Solution 4: Alternative Key Mappings**

Use different key codes for Karabiner remappings that don't conflict with HiraganaLaser.

## **Recommended Approach**

**Solution 1 (Input Source Conditional Rules)** is recommended because:

1. **Preserves Functionality**: Both Karabiner remappings and HiraganaLaser work correctly
2. **Clean Separation**: Rules only apply when appropriate
3. **Maintainable**: Easy to understand and modify
4. **Future-Proof**: Works with any additional input sources

## **Implementation Steps**

1. **Backup Current Configuration**:
   ```bash
   cp ~/.config/karabiner/karabiner.json ~/.config/karabiner/karabiner.json.backup
   ```

2. **Modify Karabiner Rules**: Add input source conditions to all remapping rules

3. **Test Both Input Sources**: Verify functionality with both ABC and HiraganaLaser

4. **Update Documentation**: Document the conditional behavior

## **Files Modified**

- `karabiner/karabiner.json` - Added to repository for tracking
- `KARABINER_CONFLICT_ANALYSIS.md` - This analysis document

## **Next Steps**

1. Implement input source conditional rules in Karabiner Elements
2. Test the modified configuration
3. Document any additional findings
4. Consider similar analysis for the copy/paste issue
