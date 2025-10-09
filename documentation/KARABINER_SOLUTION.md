# Karabiner Elements Solution for HiraganaLaser Input Source

## **Problem**
You need the Karabiner Elements remappings (F1-F12 and navigation cluster) to work when using the HiraganaLaser input source, so you can access the symbols on your keycaps.

## **Solution: Input Source Conditional Rules**

The robust solution is to modify your Karabiner Elements configuration to only apply remappings when the HiraganaLaser input source is active. This is **not fragile** because it's a standard Karabiner Elements feature.

### **Step 1: Identify Input Source Information**

From your HiraganaLaser.keylayout file:
- **Layout ID**: 16396
- **Layout Name**: HiraganaLaser666
- **Group**: 1

### **Step 2: Create Conditional Rules**

You need to modify your `karabiner.json` to add conditions that only apply when HiraganaLaser is active.

#### **Method A: Using Layout ID (Recommended)**

```json
{
  "description": "F1-F12 keycap character mappings (HiraganaLaser only)",
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
              "input_source_id": "com.apple.keylayout.HiraganaLaser666"
            }
          ]
        }
      ]
    },
    {
      "from": { "key_code": "f2" },
      "to": [{ "key_code": "1" }],
      "type": "basic",
      "conditions": [
        {
          "type": "input_source_if",
          "input_sources": [
            {
              "input_source_id": "com.apple.keylayout.HiraganaLaser666"
            }
          ]
        }
      ]
    }
    // ... continue for all F1-F12 keys
  ]
}
```

#### **Method B: Using Layout Name (Alternative)**

```json
{
  "description": "F1-F12 keycap character mappings (HiraganaLaser only)",
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
              "input_source_id": "com.apple.keylayout.HiraganaLaser666"
            }
          ]
        }
      ]
    }
    // ... continue for all keys
  ]
}
```

### **Step 3: Complete Configuration**

You need to modify **all** your existing rules to include the input source condition. Here's the pattern:

1. **F1-F12 Basic Mappings**: Add condition for HiraganaLaser only
2. **F1-F12 Shift Mappings**: Add condition for HiraganaLaser only  
3. **Navigation Cluster Basic Mappings**: Add condition for HiraganaLaser only
4. **Navigation Cluster Shift Mappings**: Add condition for HiraganaLaser only

### **Step 4: Implementation Steps**

1. **Backup Current Configuration**:
   ```bash
   cp ~/.config/karabiner/karabiner.json ~/.config/karabiner/karabiner.json.backup
   ```

2. **Modify karabiner.json**: Add the `conditions` array to each manipulator

3. **Test the Configuration**:
   - Switch to HiraganaLaser input source
   - Test F1-F12 keys - should output symbols (`, 1, 2, etc.)
   - Switch to ABC input source  
   - Test F1-F12 keys - should work as normal function keys

### **Why This Solution is Robust**

1. **Standard Feature**: Uses built-in Karabiner Elements input source conditions
2. **Not Fragile**: Doesn't modify the keyboard layout file
3. **Context-Aware**: Only applies when needed
4. **Maintainable**: Easy to understand and modify
5. **Future-Proof**: Works with system updates

### **Expected Behavior After Implementation**

- **HiraganaLaser Input Source**: F1-F12 and navigation cluster work as remapped symbols
- **ABC Input Source**: F1-F12 work as normal function keys
- **Other Input Sources**: F1-F12 work as normal function keys

### **Next Steps**

1. Implement the conditional rules in your karabiner.json
2. Test with both input sources
3. Verify the symbols on your keycaps work correctly
4. Document any issues or adjustments needed

This solution gives you exactly what you want: the Karabiner remappings work when typing in Hiragana mode, allowing you to access the symbols on your keycaps easily.
