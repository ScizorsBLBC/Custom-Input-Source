# HiraganaLaser Development Documentation

## **Project Overview**

This document provides comprehensive development documentation for the HiraganaLaser keyboard layout project, including failed approaches, edge cases discovered, testing methodologies, and best practices for future development.

## **Development History & Approaches**

### **Phase 1: Initial Development (Working Branch)**
- **Date**: 2025-01-27
- **Branch**: `working-branch`
- **Goal**: Add long vowel sound (ー) mapping to existing HiraganaLaser layout
- **Status**: ✅ **SUCCESSFUL**

#### **What Was Accomplished**
- Added Shift+む (mu) mapping for long vowel sound (ー)
- Updated XML documentation with comprehensive inline comments
- Updated README.md with new mapping and usage examples
- Fixed XML validation issues with backspace character references
- Committed changes with detailed commit messages

#### **Key Learnings**
- **XML Character References**: Backspace character `&#x0008;` caused XML validation errors
- **Solution**: Used empty output `""` for backspace to maintain functionality
- **Shift Key Pattern**: Established intuitive pattern of small characters on same keys as large counterparts

### **Phase 2: Karabiner Elements Integration (FAILED)**
- **Date**: 2025-01-27
- **Goal**: Make Karabiner Elements remappings work with HiraganaLaser input source
- **Status**: ❌ **FAILED**

#### **Problem Statement**
User needed F1-F12 and navigation cluster keys to output symbols when using HiraganaLaser input source, while maintaining normal function key behavior on other input sources.

#### **Approach 1: Input Source Conditional Rules**
```json
{
  "description": "F1 mapping for HiraganaLaser only",
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
  ]
}
```

**Why It Failed:**
- Input source ID `com.apple.keylayout.HiraganaLaser666` was incorrect
- Karabiner Elements couldn't detect the HiraganaLaser input source properly
- Input source conditions didn't activate when switching to HiraganaLaser

#### **Approach 2: Device-Specific Rules**
```json
{
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
```

**Why It Failed:**
- Device-specific rules would apply to all input sources
- Didn't solve the core problem of input source-specific behavior

#### **Approach 3: Direct Character Output**
Attempted to have Karabiner output characters directly instead of key codes.

**Why It Failed:**
- HiraganaLaser layout still intercepted the remapped key codes
- Same fundamental issue: keyboard layout processes keys before applications

### **Phase 3: Modified Keyboard Layout (FAILED)**
- **Date**: 2025-01-27
- **Goal**: Embed symbol mappings directly into HiraganaLaser layout
- **Status**: ❌ **FAILED**

#### **Approach: HiraganaLaser_with_symbols.keylayout**
Created a modified layout that included F1-F12 and navigation cluster symbol mappings.

**Key Code Mappings Attempted:**
```xml
<!-- F1-F12 Symbol Mappings -->
<key code="122" output="`"/>  <!-- F1 -> ` -->
<key code="120" output="1"/>  <!-- F2 -> 1 -->
<key code="99" output="2"/>   <!-- F3 -> 2 -->
<!-- ... etc ... -->
```

**Why It Failed:**
- Used incorrect key codes for DAS Keyboard 4 Pro
- F-keys were still being intercepted by macOS system functions
- Key code mapping didn't match actual keyboard output

#### **Key Discovery: Standard Function Keys Setting**
**Critical Finding**: The macOS setting "Use F1, F2, etc. keys as standard function keys" was **OFF**, causing F-keys to be intercepted by system functions (brightness, volume, etc.) instead of being treated as standard keys.

**Impact:**
- F-keys couldn't be remapped by Karabiner Elements
- Macro pad functionality was disabled
- Keyboard layout couldn't access F-key codes

### **Phase 4: EventViewer Analysis (PARTIAL SUCCESS)**
- **Date**: 2025-01-27
- **Goal**: Identify correct key codes for DAS Keyboard 4 Pro
- **Status**: 🔄 **PARTIAL SUCCESS**

#### **What Was Discovered**
Using Karabiner Elements EventViewer, we identified the actual key codes sent by the DAS Keyboard 4 Pro:

**F6-F12 Key Codes:**
- F6: `f6` (usage: 63)
- F7: `f7` (usage: 64)
- F8: `f8` (usage: 65)
- F9: `f9` (usage: 66)
- F10: `f10` (usage: 67)
- F11: `f11` (usage: 68)
- F12: `f12` (usage: 69)

**Navigation Cluster Key Codes:**
- Print Screen: `print_screen` (usage: 70)
- Scroll Lock: `scroll_lock` (usage: 71)
- Pause: `pause` (usage: 72)
- Insert: `insert` (usage: 73)
- Home: `home` (usage: 74)
- Page Up: `page_up` (usage: 75)
- Delete Forward: `delete_forward` (usage: 76)
- End: `end` (usage: 77)
- Page Down: `page_down` (usage: 78)

**Missing Data:**
- F1-F5 key codes were not captured in EventViewer logs
- Need to complete F1-F5 mapping for full functionality

## **Edge Cases Discovered**

### **1. USB Hub and Wireless Dongle Issues**
**Setup**: DAS Keyboard 4 Pro → USB Hub → Thunderbolt 4 → MacBook
**Issues**:
- Inconsistent copy/paste functionality (Ctrl+C, Ctrl+V)
- Macro pad functionality disabled
- Input source switching problems

**Root Cause**: USB hub latency and power delivery issues affecting keyboard input processing

### **2. Windows Keyboard on macOS**
**Setup**: DAS Keyboard 4 Pro (Windows keyboard) on macOS
**Issues**:
- Command/Option key positions reversed
- F-key behavior different from Mac keyboards
- System function key interception

**Solutions Implemented**:
- Karabiner Elements Command/Option swap rules
- Enable "Use F1, F2, etc. keys as standard function keys" setting

### **3. Input Source Detection Problems**
**Issue**: Karabiner Elements couldn't properly detect HiraganaLaser input source
**Symptoms**:
- Input source conditional rules didn't activate
- Rules worked on ABC input source but not HiraganaLaser
- EventViewer showed correct key codes but rules didn't apply

**Investigation**: Input source ID format and detection mechanism issues

### **4. Keyboard Layout vs. Karabiner Elements Conflict**
**Core Problem**: Keyboard layouts process keys before Karabiner Elements
**Processing Order**: Hardware → Karabiner Elements → Keyboard Layout → Application
**Result**: HiraganaLaser layout intercepted Karabiner-remapped keys and output Hiragana characters instead of intended symbols

## **Testing Methodology & Best Practices**

### **Test Environment Setup**
```
/Users/scizors/Library/Keyboard Layouts/
├── HiraganaLaser.keylayout              # Production layout
├── test-layouts/                        # Test layout versions
│   ├── HiraganaLaser_with_symbols.keylayout
│   ├── HiraganaLaser_fixed.keylayout
│   └── HiraganaLaser_conditional.keylayout
├── karabiner/                           # Karabiner Elements configs
│   ├── karabiner.json                   # Production config
│   ├── karabiner.json.backup            # Backup
│   ├── command_option_swap.json         # Command/Option swap
│   ├── f1_f12_hiragana_only.json        # F-key mappings
│   └── test_rules/                      # Test rule variations
└── documentation/                       # Development docs
    ├── DEVELOPMENT_README.md            # This file
    ├── KARABINER_CONFLICT_ANALYSIS.md   # Conflict analysis
    └── KARABINER_SOLUTION.md            # Solution attempts
```

### **Testing Protocol**

#### **1. Layout Testing**
```bash
# Backup current layout
cp ~/Library/Keyboard\ Layouts/HiraganaLaser.keylayout ~/Library/Keyboard\ Layouts/HiraganaLaser.keylayout.backup

# Test new layout
cp test-layouts/HiraganaLaser_test.keylayout ~/Library/Keyboard\ Layouts/HiraganaLaser.keylayout

# Restart system
sudo reboot
# OR
# Log out and back in
```

#### **2. Karabiner Elements Testing**
```bash
# Backup current config
cp ~/.config/karabiner/karabiner.json ~/.config/karabiner/karabiner.json.backup

# Test new config
cp karabiner/test_config.json ~/.config/karabiner/karabiner.json

# Reload Karabiner Elements
# (Auto-reloads, or restart Karabiner Elements)
```

#### **3. Input Source Testing**
1. **Switch to ABC input source**
2. **Test all F-keys and navigation cluster**
3. **Switch to HiraganaLaser input source**
4. **Test all F-keys and navigation cluster**
5. **Test Hiragana character typing**
6. **Test Shift combinations**

#### **4. EventViewer Analysis**
1. **Open Karabiner Elements EventViewer**
2. **Switch to target input source**
3. **Press each key systematically**
4. **Record key codes and usage values**
5. **Compare with expected mappings**

### **Test Data Collection**

#### **Key Code Mapping Table**
| Physical Key | Expected Output | Actual Key Code | Usage Value | Status |
|--------------|----------------|-----------------|-------------|---------|
| F1 | ` | ? | ? | ❌ Missing |
| F2 | 1 | ? | ? | ❌ Missing |
| F3 | 2 | ? | ? | ❌ Missing |
| F4 | 3 | ? | ? | ❌ Missing |
| F5 | 4 | ? | ? | ❌ Missing |
| F6 | 5 | f6 | 63 | ✅ Captured |
| F7 | 6 | f7 | 64 | ✅ Captured |
| F8 | 7 | f8 | 65 | ✅ Captured |
| F9 | 8 | f9 | 66 | ✅ Captured |
| F10 | 9 | f10 | 67 | ✅ Captured |
| F11 | 0 | f11 | 68 | ✅ Captured |
| F12 | \ | f12 | 69 | ✅ Captured |

#### **Navigation Cluster Mapping Table**
| Physical Key | Expected Output | Actual Key Code | Usage Value | Status |
|--------------|----------------|-----------------|-------------|---------|
| Print Screen | - | print_screen | 70 | ✅ Captured |
| Scroll Lock | = | scroll_lock | 71 | ✅ Captured |
| Pause | [ | pause | 72 | ✅ Captured |
| Insert | ; | insert | 73 | ✅ Captured |
| Home | ' | home | 74 | ✅ Captured |
| Page Up | ] | page_up | 75 | ✅ Captured |
| Delete Forward | , | delete_forward | 76 | ✅ Captured |
| End | . | end | 77 | ✅ Captured |
| Page Down | / | page_down | 78 | ✅ Captured |

## **Failed Approaches Analysis**

### **1. Input Source Conditional Rules**
**Why It Failed:**
- Incorrect input source ID format
- Karabiner Elements couldn't detect custom keyboard layouts properly
- Input source switching mechanism issues

**Lessons Learned:**
- Always verify input source IDs using EventViewer
- Test input source detection before implementing conditional rules
- Consider alternative approaches when input source detection fails

### **2. Modified Keyboard Layout**
**Why It Failed:**
- Incorrect key code mappings for specific keyboard model
- F-key system function interception
- Key code format mismatch (string vs. numeric)

**Lessons Learned:**
- Always use EventViewer to identify actual key codes
- Test with "Use F1, F2, etc. keys as standard function keys" enabled
- Verify key code format compatibility

### **3. Device-Specific Rules**
**Why It Failed:**
- Would apply to all input sources, not just HiraganaLaser
- Didn't solve the core input source-specific requirement

**Lessons Learned:**
- Device-specific rules are too broad for input source-specific needs
- Consider the scope of rule application before implementation

## **Current Status & Next Steps**

### **What Works**
- ✅ HiraganaLaser layout with long vowel sound (ー) mapping
- ✅ Command/Option key swap for Windows keyboard
- ✅ Basic F-key functionality with standard function keys enabled
- ✅ EventViewer key code identification for F6-F12 and navigation cluster

### **What Doesn't Work**
- ❌ F1-F5 symbol mapping (key codes not identified)
- ❌ Input source conditional rules
- ❌ Karabiner Elements integration with HiraganaLaser
- ❌ Copy/paste functionality with USB hub setup

### **Immediate Next Steps**
1. **Complete F1-F5 key code identification** using EventViewer
2. **Test modified layout approach** with correct key codes
3. **Investigate USB hub copy/paste issues** separately
4. **Consider alternative approaches** for input source-specific behavior

### **Long-term Solutions**
1. **Hybrid approach**: Use different input sources for different purposes
2. **Layout modification**: Embed all symbol mappings directly in layout
3. **Hardware solution**: Use different keyboard or connection method
4. **Software solution**: Develop custom input method bundle

## **Development Best Practices**

### **1. Version Control**
- Always work on feature branches, never on main
- Use descriptive commit messages with scope and impact
- Keep test layouts in separate directory
- Document all changes in development README

### **2. Testing Protocol**
- Test on clean system state (restart after layout changes)
- Use EventViewer for key code identification
- Test both input sources systematically
- Document all test results and failures

### **3. Documentation Standards**
- Enterprise-grade inline comments in all files
- Comprehensive README updates for user-facing changes
- Detailed development documentation for technical changes
- Clear troubleshooting guides for common issues

### **4. File Organization**
```
project/
├── production/           # Production-ready files
├── test-layouts/         # Test layout versions
├── karabiner/           # Karabiner Elements configs
├── documentation/       # Development documentation
└── backups/            # Backup files
```

### **5. Error Handling**
- Always backup before making changes
- Test incrementally, not all at once
- Document error messages and solutions
- Keep rollback procedures ready

## **Technical Specifications**

### **System Requirements**
- **macOS**: 15.7.1 (tested)
- **Keyboard**: DAS Keyboard 4 Pro (Windows)
- **Connection**: USB Hub → Thunderbolt 4 → MacBook
- **Software**: Karabiner Elements, Ukelele

### **Key Dependencies**
- Apple KeyboardLayout.dtd v1.0
- Karabiner Elements for key remapping
- macOS Input Sources system
- UTF-8 encoding for Japanese characters

### **Known Limitations**
- F1-F5 key codes not identified
- Input source conditional rules don't work
- USB hub causes copy/paste issues
- Windows keyboard requires Command/Option swap

## **Conclusion**

The HiraganaLaser project successfully implemented the core functionality (Hiragana typing with long vowel sound) but encountered significant challenges with Karabiner Elements integration and symbol mapping. The development process revealed important insights about macOS keyboard input processing, USB hub limitations, and the complexity of input source-specific behavior.

Future development should focus on completing the F1-F5 key code identification and testing the modified layout approach with correct key codes. The hybrid approach of using different input sources for different purposes may be the most practical solution given the current limitations.

---

**Last Updated**: 2025-01-27  
**Branch**: working-branch  
**Status**: Development ongoing  
**Next Review**: After F1-F5 key code identification
