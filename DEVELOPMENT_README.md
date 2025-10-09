# HiraganaLaser Development Documentation

## **Project Overview**

This document provides comprehensive development documentation for the HiraganaLaser keyboard layout project, including failed approaches, edge cases discovered, and best practices for testing and development.

## **Project Evolution**

### **Original Goal**
Create a custom macOS keyboard layout that enables direct Hiragana character input while maintaining access to symbol mappings on F1-F12 and navigation cluster keys through Karabiner Elements integration.

### **Final Implementation**
- **Input Source Name**: ひらがな (Hiragana)
- **Layout File**: `Hiragana.keylayout`
- **Layout ID**: 16396
- **Group**: 1

## **Development Approaches Attempted**

### **Approach 1: Karabiner Elements Input Source Conditional Rules**

**Goal**: Use Karabiner Elements to remap F1-F12 and navigation cluster keys only when using the HiraganaLaser input source.

**Implementation**:
- Created conditional rules using `input_source_if` conditions
- Attempted to use `com.apple.keylayout.HiraganaLaser666` as input source ID
- Tried multiple input source ID formats

**Why It Failed**:
1. **Input Source ID Mismatch**: The actual input source ID didn't match our assumptions
2. **Key Code Interception**: HiraganaLaser layout intercepted Karabiner-remapped key codes before they could reach applications
3. **Processing Order**: macOS processes keyboard input as: Hardware → Karabiner → Keyboard Layout → Application, causing conflicts

**Key Learning**: Custom keyboard layouts intercept and override Karabiner Elements remappings, making conditional remapping impossible.

### **Approach 2: Modified Keyboard Layout with Symbol Mappings**

**Goal**: Embed symbol mappings directly into the keyboard layout file, eliminating the need for Karabiner Elements.

**Implementation**:
- Created `HiraganaLaser_with_symbols.keylayout` with F1-F12 and navigation cluster symbol mappings
- Used numeric key codes (122, 120, 99, etc.) for F-keys
- Mapped navigation cluster keys to symbols

**Why It Failed**:
1. **Incorrect Key Codes**: Used wrong key codes for DAS Keyboard 4 Pro
2. **F-Key System Override**: macOS "Use F1, F2, etc. keys as standard function keys" setting was disabled
3. **Key Code Mismatch**: EventViewer showed different key codes than expected

**Key Learning**: Must verify actual key codes from EventViewer for specific keyboard models.

### **Approach 3: EventViewer-Based Key Code Correction**

**Goal**: Use Karabiner Elements EventViewer to identify correct key codes and create accurate mappings.

**Implementation**:
- Analyzed EventViewer logs for DAS Keyboard 4 Pro
- Identified correct key codes: `f6`, `f7`, `f8`, etc. (string format)
- Created `HiraganaLaser_fixed.keylayout` with corrected mappings

**Why It Failed**:
1. **Incomplete Key Code Data**: Missing F1-F5 key codes from EventViewer logs
2. **Layout File Corruption**: Multiple layout file versions caused conflicts
3. **System Integration Issues**: Layout changes required system restart to take effect

**Key Learning**: Complete key code mapping is essential; partial mappings cause unpredictable behavior.

## **Edge Cases Discovered**

### **Edge Case 1: USB Hub and Wireless Dongle Interference**

**Description**: Macro pad connected via 2.4GHz wireless dongle through USB-C hub to Thunderbolt 4 connection caused intermittent input issues.

**Symptoms**:
- Copy/paste functionality inconsistent across applications
- Some applications only accepted input from laptop keyboard
- Macro pad hotkeys (Ctrl+C, Ctrl+V) stopped working

**Root Cause**: USB hub power delivery and timing issues with wireless dongle input processing.

**Resolution**: Direct connection testing isolated the issue to USB hub configuration.

### **Edge Case 2: macOS F-Key System Override**

**Description**: "Use F1, F2, etc. keys as standard function keys" setting in System Settings affected both Karabiner Elements and keyboard layout functionality.

**Symptoms**:
- F-keys performed system functions (brightness, volume) instead of character output
- Karabiner Elements remappings didn't work
- Macro pad screenshot hotkey disabled

**Root Cause**: macOS intercepts F-keys for system functions when standard function keys setting is disabled.

**Resolution**: Enable "Use F1, F2, etc. keys as standard function keys" in System Settings.

### **Edge Case 3: Input Source ID Format Variations**

**Description**: Different input source ID formats required for different macOS versions and input source types.

**Attempted Formats**:
- `com.apple.keylayout.HiraganaLaser666`
- `HiraganaLaser666`
- `com.apple.inputmethod.Kotoeri.Hiragana`

**Root Cause**: Input source IDs vary by macOS version and input source type (keyboard layout vs. input method).

**Resolution**: Use EventViewer to identify correct input source ID format.

### **Edge Case 4: Command/Option Key Swap for Windows Keyboards**

**Description**: DAS Keyboard 4 Pro (Windows keyboard) on macOS required Command/Option key swapping.

**Symptoms**:
- Command key (Windows key) didn't work as expected
- Option key behavior was inverted

**Resolution**: Implemented Karabiner Elements rules to swap Command and Option keys:
```json
{
  "from": { "key_code": "left_command" },
  "to": [{ "key_code": "left_option" }],
  "type": "basic"
}
```

## **Testing Best Practices**

### **File Organization**

**Test Directory Structure**:
```
/Users/scizors/Library/Keyboard Layouts/
├── Hiragana.keylayout                    # Production layout
├── test-layouts/                         # Test versions
│   ├── Hiragana_test1.keylayout
│   ├── Hiragana_test2.keylayout
│   └── Hiragana_backup.keylayout
├── karabiner/                           # Karabiner Elements configs
│   ├── karabiner.json
│   └── karabiner.json.backup
└── DEVELOPMENT_README.md                # This file
```

**Best Practices**:
1. **Always backup** production files before testing
2. **Use test directory** for experimental layouts
3. **Version control** all configuration files
4. **Document changes** in commit messages

### **Testing Workflow**

**Step 1: Environment Setup**
1. Enable "Use F1, F2, etc. keys as standard function keys"
2. Verify input source is properly installed
3. Check Karabiner Elements is running

**Step 2: Key Code Verification**
1. Use EventViewer to identify actual key codes
2. Test both ABC and target input sources
3. Verify key codes are consistent

**Step 3: Layout Testing**
1. Install test layout in test directory
2. Copy to production location
3. Restart system or log out/in
4. Test all mapped keys

**Step 4: Integration Testing**
1. Test with Karabiner Elements active
2. Test with different applications
3. Test with USB hub and external devices

### **Debugging Tools**

**Karabiner Elements EventViewer**:
- **Purpose**: Identify actual key codes and input source IDs
- **Usage**: Monitor key presses and input source changes
- **Location**: Karabiner Elements → EventViewer tab

**System Console**:
- **Purpose**: Monitor system-level keyboard input processing
- **Usage**: Filter for keyboard-related messages
- **Location**: Applications → Utilities → Console

**Input Source Verification**:
```bash
defaults read com.apple.HIToolbox AppleEnabledInputSources
defaults read com.apple.HIToolbox AppleSelectedInputSources
```

## **Technical Specifications**

### **Keyboard Layout File Format**

**File Structure**:
```xml
<?xml version="1.1" encoding="UTF-8"?>
<!DOCTYPE keyboard SYSTEM "file://localhost/System/Library/DTDs/KeyboardLayout.dtd">
<keyboard group="1" id="16396" name="ひらがな" maxout="2">
    <layouts>
        <layout first="0" last="1" mapSet="ANSI" modifiers="modifierMap0"/>
    </layouts>
    <modifierMap id="modifierMap0" defaultIndex="0">
        <keyMapSelect mapIndex="0">
            <modifier keys=""/>
        </keyMapSelect>
        <keyMapSelect mapIndex="1">
            <modifier keys="shift"/>
        </keyMapSelect>
    </modifierMap>
    <keyMapSet id="ANSI">
        <keyMap index="0">
            <!-- Base key mappings -->
        </keyMap>
        <keyMap index="1">
            <!-- Shift key mappings -->
        </keyMap>
    </keyMapSet>
</keyboard>
```

**Key Requirements**:
- **XML Version**: 1.1 for Ukelele compatibility
- **Encoding**: UTF-8 for Japanese characters
- **DTD**: Apple KeyboardLayout.dtd v1.0
- **Layout ID**: Must be unique (16396)
- **Group**: 1 for keyboard group identifier

### **Key Code Mapping**

**DAS Keyboard 4 Pro Key Codes**:
- **F6-F12**: `f6`, `f7`, `f8`, `f9`, `f10`, `f11`, `f12`
- **Navigation Cluster**: `print_screen`, `scroll_lock`, `pause`, `insert`, `home`, `page_up`, `delete_forward`, `end`, `page_down`
- **Standard Keys**: 0-53 range for QWERTY keys

**Key Code Format**:
- **String Format**: `f1`, `f2`, etc. (preferred for F-keys)
- **Numeric Format**: 122, 120, etc. (for standard keys)
- **Usage**: String format for Karabiner Elements, numeric format for keyboard layouts

## **Current Status**

### **Working Components**
- ✅ Command/Option key swap via Karabiner Elements
- ✅ Hiragana character input on standard keys
- ✅ Input source switching between ABC and ひらがな
- ✅ System integration and installation

### **Outstanding Issues**
- ❌ F1-F12 symbol mappings (incomplete key code data)
- ❌ Navigation cluster symbol mappings (key code mismatch)
- ❌ Copy/paste functionality with USB hub setup
- ❌ Macro pad integration with custom layout

### **Next Steps**
1. **Complete F1-F5 key code identification** using EventViewer
2. **Create comprehensive key code mapping** for all target keys
3. **Implement symbol mappings** in keyboard layout file
4. **Test with complete USB hub setup** including macro pad
5. **Document final working configuration**

## **Lessons Learned**

### **Technical Lessons**
1. **Keyboard layouts override Karabiner Elements** - cannot use conditional remapping
2. **Key codes vary by keyboard model** - always verify with EventViewer
3. **System settings affect F-key behavior** - check "Use F1, F2, etc. keys as standard function keys"
4. **Input source IDs are version-specific** - use EventViewer to identify correct format

### **Process Lessons**
1. **Test incrementally** - verify each component before integration
2. **Document everything** - edge cases and failures are valuable
3. **Use version control** - track all configuration changes
4. **Backup before testing** - prevent configuration loss

### **Hardware Lessons**
1. **USB hub compatibility** - test with direct connection first
2. **Wireless dongle timing** - power delivery affects input processing
3. **Keyboard model differences** - key codes vary by manufacturer
4. **macOS version compatibility** - input source handling changes

## **File Inventory**

### **Production Files**
- `Hiragana.keylayout` - Main keyboard layout file
- `README.md` - User documentation
- `LICENSE` - CC0-1.0 license

### **Development Files**
- `DEVELOPMENT_README.md` - This development documentation
- `KARABINER_CONFLICT_ANALYSIS.md` - Karabiner Elements conflict analysis
- `KARABINER_SOLUTION.md` - Proposed Karabiner Elements solution
- `COMBINING_CHARACTERS_SUMMARY.md` - Combining characters implementation

### **Configuration Files**
- `karabiner/karabiner.json` - Karabiner Elements configuration
- `karabiner/karabiner.json.backup` - Backup configuration

### **Test Files**
- `test-layouts/` - Directory for experimental layouts
- Various test layout files (deleted after testing)

## **Contributing Guidelines**

### **Code Standards**
- **Enterprise-grade documentation** for all files
- **Comprehensive inline comments** explaining technical decisions
- **Version control** with descriptive commit messages
- **Testing documentation** for all changes

### **Testing Requirements**
- **Test on clean system** before committing changes
- **Verify with EventViewer** for key code accuracy
- **Test with multiple input sources** and applications
- **Document test results** and any issues found

### **Documentation Standards**
- **Update README.md** for user-facing changes
- **Update DEVELOPMENT_README.md** for technical changes
- **Include troubleshooting** for common issues
- **Document edge cases** and workarounds

---

**Last Updated**: 2025-01-27  
**Version**: 1.0  
**Status**: In Development
