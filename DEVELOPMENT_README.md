# ひらがな-カタカナ Development Documentation

# **note: カタカナ has not been fully tested and compared to the keymapping of the DROP WOB Katakana GMK keycap set**

## **Project Overview**

This document provides comprehensive development documentation for the HiraganaLaser keyboard layout project, including failed approaches, edge cases discovered, and best practices for testing and development.

## **Project Evolution**

### **Original Goal**
Create a custom macOS keyboard layout that enables direct Hiragana character input while maintaining access to symbol mappings on F1-F12 and navigation cluster keys through Karabiner Elements integration.

### **Final Implementation**
- **Input Source Name**: ひらがな-カタカナ (Hiragana-Katakana)
- **Layout File**: `Hiragana_Katakana.keylayout`
- **Layout ID**: 16396
- **Group**: 1
- **Dual-Mode Layout**: Caps Lock toggle between Hiragana (OFF) and Katakana (ON) modes
- **Four-Layer System**: Each mode has its own Shift layer for small characters and special symbols

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

## **Critical Bug: Numpad Key 86 Crash Issue**

### **Problem Description**

**Severity**: CRITICAL - Causes application crashes
**Affected Key**: Numpad 4 (key code 86, usage 0x0056)
**Affected Applications**: Chrome, and potentially other applications
**Crash Type**: `EXC_BREAKPOINT (SIGTRAP)` in `-[NSMenu performKeyEquivalent:]`

### **Crash Analysis**

**Crash Location**:
```
Thread 0 Crashed:: CrBrowserMain Dispatch queue: com.apple.main-thread
0   AppKit                        0x1951fc628 -[NSApplication _crashOnException:] + 256
1   AppKit                        0x1951fc3e8 -[NSApplication reportException:] + 460
2   AppKit                        0x1954c441c NSApplicationUncaughtExceptionHandler + 152
3   CoreFoundation                0x191127078 __handleUncaughtException + 820
4   libobjc.A.dylib               0x190b44dc8 _objc_terminate() + 144
5   libc++abi.dylib               0x190ed0698 std::__terminate(void (*)()) + 16
6   libc++abi.dylib               0x190ed3c30 __cxxabiv1::failed_throw(__cxxabiv1::__cxa_exception*) + 88
7   libc++abi.dylib               0x190ed3bd8 __cxa_throw + 92
8   libobjc.A.dylib               0x190b3acf8 objc_exception_throw + 448
9   CoreFoundation                0x191172084 _CFThrowFormattedException + 124
10  CoreFoundation                0x1911720bc -[__NSCFString characterAtIndex:].cold.1 + 56
11  CoreFoundation                0x190fe1aa8 -[__NSCFString characterAtIndex:] + 124
12  AppKit                        0x1951901d0 -[NSMenu performKeyEquivalent:] + 80
```

**Root Cause**: macOS's menu keyboard shortcut matching system encounters a string bounds exception when processing key code 86. The issue occurs in `-[__NSCFString characterAtIndex:]` when trying to read characters from the key output string.

### **Attempted Solutions**

#### **Solution 1: Remap to = and + Symbols (FAILED)**

**Implementation**: 
- Changed key code 86 from outputting "4" and "$" to "=" and "+"
- Applied across all modifier states (base, shift, caps lock, caps+shift)
- Added comprehensive documentation

**Result**: **STILL CRASHES** - The issue persists even with proper character outputs

**Analysis**: The problem is not with the specific characters being output, but rather with how macOS processes numpad keys in custom keyboard layouts when Caps Lock is active.

#### **Solution 2: Investigation Findings**

**Key Discovery**: The crash occurs specifically when:
1. Using the Hiragana-Katakana input source
2. Caps Lock is active (Katakana mode)
3. Pressing numpad 4 key (key code 86)
4. macOS tries to match the key against menu shortcuts

**Technical Details**:
- **Key Code**: 86 (0x0056) - Numpad 4
- **Usage Page**: 7 (0x0007) - Keyboard/Keypad
- **Usage**: 86 (0x0056) - Keypad 4
- **Crash Location**: NSMenu keyboard shortcut matching code

### **Current Status**

**Status**: UNRESOLVED - Critical bug still present
**Impact**: Prevents safe use of numpad 4 key in any application
**Workaround**: Avoid using numpad 4 key when Caps Lock is active

### **Investigation Notes**

1. **Not a Character Issue**: The crash occurs regardless of what characters are mapped to key code 86
2. **Caps Lock Specific**: Only happens when Caps Lock is active (Katakana mode)
3. **System-Level Issue**: The problem is in macOS's menu shortcut matching, not our layout
4. **Numpad Key Specific**: Only affects numpad keys, not main keyboard keys

### **Potential Solutions to Investigate**

1. **Empty Output Mapping**: Try mapping key code 86 to empty string `""` in all layers
2. **Control Character Mapping**: Map to a control character instead of printable characters
3. **System Key Mapping**: Map to a system key that doesn't trigger menu matching
4. **Layout Structure Issue**: Investigate if the issue is with our layout's modifier map structure
5. **macOS Version Specific**: Test on different macOS versions to see if it's version-specific

### **Testing Protocol**

**Required Tests**:
1. Test numpad 4 key in Chrome with Caps Lock OFF (should work)
2. Test numpad 4 key in Chrome with Caps Lock ON (currently crashes)
3. Test other numpad keys (82-85, 87-92) with Caps Lock ON
4. Test in multiple applications (TextEdit, Terminal, Safari)
5. Test with different keyboard layouts to isolate the issue

**Test Commands**:
```bash
# Test in Terminal
echo "Testing numpad 4 with Caps Lock ON"
# Press numpad 4 key here

# Test in TextEdit
# Open TextEdit, enable Caps Lock, press numpad 4
```

### **Documentation Updates Needed**

1. **README.md**: Add warning about numpad 4 key crash
2. **Installation Guide**: Include workaround instructions
3. **Known Issues**: Document this as a critical known issue
4. **Troubleshooting**: Add crash resolution steps

### **Next Steps**

1. **Immediate**: Document this as a critical known issue
2. **Short-term**: Implement workaround (empty output mapping)
3. **Medium-term**: Investigate alternative layout structures
4. **Long-term**: Report to Apple as a potential macOS bug

## **Current Status**

### **Working Components**
- ✅ Command/Option key swap via Karabiner Elements
- ✅ Hiragana character input on standard keys (Caps Lock OFF)
- ✅ Katakana character input on standard keys (Caps Lock ON)
- ✅ Caps Lock toggle between Hiragana and Katakana modes
- ✅ Four-layer system with independent Shift layers for each mode
- ✅ Small character support in both Hiragana and Katakana modes
- ✅ Combining characters (dakuten/handakuten) work in both modes
- ✅ Input source switching between ABC and ひらがな-カタカナ
- ✅ System integration and installation

### **Outstanding Issues**
- ❌ **CRITICAL**: Numpad 4 key crash in BOTH Hiragana and Katakana modes
- ❌ F1-F12 symbol mappings (incomplete key code data)
- ❌ Navigation cluster symbol mappings (key code mismatch)
- ❌ Copy/paste functionality with USB hub setup
- ❌ Macro pad integration with custom layout

### **Caps Lock Layer Implementation**

The dual-mode layout uses Caps Lock as a persistent toggle between Hiragana and Katakana modes:

#### **Technical Implementation**
- **Modifier Map**: Uses `caps` and `anyShift caps` modifiers for Katakana layers
- **Layer Structure**: Four distinct keyMap indices (0-3) for complete functionality
- **Toggle Behavior**: Caps Lock acts as a locking modifier (persistent until pressed again)
- **LED Indication**: Caps Lock LED shows which mode is active

#### **Layer Mapping**
- **Layer 0**: Hiragana Base (Caps Lock OFF, no modifiers)
- **Layer 1**: Hiragana Shift (Caps Lock OFF + Shift)
- **Layer 2**: Katakana Base (Caps Lock ON, no modifiers)
- **Layer 3**: Katakana Shift (Caps Lock ON + Shift)

#### **Character Mapping Strategy**
- **Parallel Mapping**: Same QWERTY key produces corresponding Hiragana/Katakana
- **Intuitive Learning**: Visual correspondence between scripts aids learning
- **Consistent Behavior**: Shift layers work identically in both modes
- **Complete Coverage**: All 46 basic characters plus small characters and symbols

### **Next Steps**
1. **URGENT**: Resolve numpad 4 crash issue affecting both modes
2. **Complete F1-F5 key code identification** using EventViewer
3. **Create comprehensive key code mapping** for all target keys
4. **Implement symbol mappings** in keyboard layout file
5. **Test with complete USB hub setup** including macro pad
6. **Document final working configuration**

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
- `Hiragana_Katakana.keylayout` - Main dual-mode keyboard layout file
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
