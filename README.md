# HiraganaLaser - Enterprise-Grade Custom Japanese Input Source

## **Project Overview**

HiraganaLaser is a production-ready macOS keyboard layout that enables direct typing of Hiragana characters on QWERTY keyboards, designed for Japanese language learning and efficient text input. This enterprise-grade solution provides comprehensive Hiragana character coverage with optimized key mapping strategies.

### **Key Features**
- **Complete Hiragana Set**: All 46 basic Hiragana characters mapped
- **Intuitive Shift Mappings**: Small characters on same keys as large counterparts
- **Complete Small Character Set**: All essential small hiragana (ぁぃぅぇぉゃゅょっ)
- **Direct Input Method**: No IME conversion required
- **Enterprise Documentation**: Comprehensive technical specifications
- **Dual Implementation**: Simple keyboard layout + advanced input method bundle
- **Learning Optimized**: Character frequency-based mapping for efficient learning

### **Target Hardware**
Designed for custom mechanical keyboards with Hiragana legends, specifically the DROP x MiTo Laser R2 GMK 'Kobe' Hiragana legends keycaps or compatible sets.

![DROP x MiTo Laser R2 Kobe Hiragana set](DROP_x_MiTo_Laser_R2_Kobe_Hiragana_set.png)

## Overview

This project is designed to aid in learning Japanese Hiragana characters by using a direct typing input method instead of traditional Romaji or Kana IME conversion input methods. It provides a working macOS input source that maps QWERTY keys directly to Hiragana characters, enabling direct Japanese text input without IME conversion.

## Features

✅ **Complete Hiragana Character Set** - All 46 basic Hiragana characters mapped  
✅ **Number Row Support** - Numbers 0-9 mapped to Hiragana characters  
✅ **ANSI Keyboard Layout** - Correct functionality for all other ANSI keys  
✅ **macOS Integration** - Works with System Preferences Input Sources  
✅ **UTF-8 Encoding** - Proper Japanese character support  

## Installation (3 Options)

### **Install Method 1: Direct Installation (1st Recommended Option)**

1. **Download the layout file:**
   - Copy `HiraganaLaser.keylayout` to `~/Library/Keyboard Layouts/`

2. **Restart your Mac:**
   - Log out and back in, or restart completely

3. **Add to Input Sources:**
   - Go to System Preferences > Keyboard > Input Sources
   - Click the "+" button
   - Find "HiraganaLaser" in the list and add it

4. **Select the layout:**
   - Use the input source menu in your menu bar to switch to HiraganaLaser

## **-OR-**

### **Install Method 2: Ukelele Direct Install (2nd Recommended Option)**

For the easiest installation using Ukelele's built-in installer:

1. **Download Ukelele** from [software.sil.org/ukelele](https://software.sil.org/ukelele/)
2. **Open the layout:** File → Open → Select `HiraganaLaser.keylayout`
3. **Install directly:** File → Install (see screenshot below)
4. **Restart your Mac** to activate the input source
5. **Add to Input Sources:** Go to System Preferences > Keyboard > Input Sources and add "HiraganaLaser"

![Ukelele Install Menu](Ukelele_Install_Menu.png)

## **-OR-**

### **Install Method 3: Ukelele Bundle (Alternative)**

If you prefer to create a bundle manually:

1. **Download Ukelele** from [software.sil.org/ukelele](https://software.sil.org/ukelele/)
2. **Open the layout:** File → Open → Select `HiraganaLaser.keylayout`
3. **Set keyboard name:** File → Set Keyboard Name → "HiraganaLaser"
4. **Save as bundle:** File → Save As Bundle → Save as `HiraganaLaser.bundle`
5. **Install:** Copy the bundle to `~/Library/Keyboard Layouts/`
6. **Restart** and add to Input Sources as above

## Key Mapping

### **macOS Key Code Reference**

**Important**: In macOS keyboard layouts, key codes correspond to **physical key positions** on a US QWERTY keyboard, not the characters they produce. This reference table shows the correct key codes for each physical key position.

#### **Complete Key Code Mapping Table**

| Physical Key | Key Code | Hiragana Output | Notes |
|--------------|----------|-----------------|-------|
| **Number Row** | | | |
| ` | 50 | ろ (ro) | Backtick key |
| 1 | 18 | ぬ (nu) | |
| 2 | 19 | ふ (fu) | |
| 3 | 20 | あ (a) | |
| 4 | 21 | う (u) | |
| 5 | 23 | え (e) | |
| 6 | 22 | お (o) | |
| 7 | 26 | や (ya) | |
| 8 | 28 | ゆ (yu) | |
| 9 | 25 | よ (yo) | |
| 0 | 29 | わ (wa) | |
| - | 27 | ほ (ho) | |
| = | 24 | へ (he) | |
| **Top Row** | | | |
| Q | 12 | た (ta) | |
| W | 13 | て (te) | |
| E | 14 | い (i) | |
| R | 15 | す (su) | |
| T | 17 | か (ka) | |
| Y | 16 | ん (n) | |
| U | 32 | な (na) | |
| I | 34 | に (ni) | |
| O | 31 | ら (ra) | |
| P | 35 | せ (se) | |
| [ | 33 | ゙ (dakuten) | Combining character |
| ] | 30 | ゚ (handakuten) | Combining character |
| \ | 42 | む (mu) | |
| **Home Row** | | | |
| A | 0 | ち (chi) | |
| S | 1 | と (to) | |
| D | 2 | し (shi) | |
| F | 3 | は (ha) | |
| G | 5 | き (ki) | |
| H | 4 | く (ku) | |
| J | 38 | ま (ma) | |
| K | 40 | の (no) | |
| L | 37 | り (ri) | |
| ; | 41 | れ (re) | |
| ' | 39 | け (ke) | |
| **Bottom Row** | | | |
| Z | 6 | つ (tsu) | |
| X | 7 | さ (sa) | |
| C | 8 | そ (so) | |
| V | 9 | ひ (hi) | |
| B | 11 | こ (ko) | |
| N | 45 | み (mi) | |
| M | 46 | も (mo) | |
| , | 43 | ね (ne) | |
| . | 47 | る (ru) | |
| / | 44 | め (me) | |
| **Control Keys** | | | |
| Tab | 48 | Tab character | Preserved functionality |
| Space | 49 | Space character | Preserved functionality |
| Backspace | 51 | Backspace character | Preserved functionality |
| Enter | 36 | Carriage Return | Preserved functionality |
| Escape | 53 | Escape character | Preserved functionality |

#### **Shift Key Mappings (Small Characters)**

| Physical Key | Key Code | Shift+Output | Notes |
|--------------|----------|--------------|-------|
| **Number Row** | | | |
| 0 | 29 | を (wo) | Object particle (on same key as わ) |
| 3 | 20 | ぁ (small あ) | Small vowel character |
| 4 | 21 | ぅ (small う) | Small vowel character |
| 5 | 23 | ぇ (small え) | Small vowel character |
| 6 | 22 | ぉ (small お) | Small vowel character |
| 7 | 26 | ゃ (small や) | Small ya character |
| 8 | 28 | ゅ (small ゆ) | Small yu character |
| 9 | 25 | ょ (small よ) | Small yo character |
| **Top Row** | | | |
| E | 14 | ぃ (small い) | Small vowel character |
| **Bottom Row** | | | |
| Z | 6 | っ (small つ) | Small tsu for double consonants |

**Note**: Small characters are placed on the same keys as their large counterparts for intuitive access. Only essential small characters are mapped, avoiding duplicate or confusing mappings.

### **Working Key Mapping (Left to Right, Top to Bottom)**

#### **Number Row**
|    `    |    1    |    2   |    3   |   4   |   5    |    6   |    7   |    8    |    9    |    0   |    -    |    =    |
|---------|---------|--------|--------|-------|--------|--------|--------|---------|---------|--------|---------|---------|
| ろ (ro) | ぬ (nu) | ふ (fu) | あ (a) | う (u) | え (e) | お (o) | や (ya) | ゆ (yu) | よ (yo) | わ (wa) | ほ (ho) | へ (he) |

#### **Top Row**
|    q    |    w    |   e    |    r   |   t   |   y    |    u    |    i   |    o    |    p    |    [   |    ]     |    \    |
|---------|---------|--------|--------|-------|--------|---------|--------|---------|---------|--------|----------|---------|
| た (ta) | て (te) | い (i)  | す (su)| か (a) | ん (n) | な (na) | に (ni) | ら (ra) | せ (se) | ゛(dkt) | ゜ (hdk) | む (mu) |



#### **Home Row**
|    a     |    s    |    d    |    f    |    g   |    h    |     j   |    k   |    l    |    ;    |    '   |
|----------|---------|---------|---------|--------|---------|---------|--------|---------|---------|--------|
| ち (chi) | と (to) | し (shi) | は (ha) | き (ki) | く (ku) | ま (ma) | の (no) | り (ri) | れ (re) | け (ke) |


#### **Bottom Row**
|     z    |    x    |   c    |     v   |    b   |    n    |    m    |    ,   |    .    |    /    |
|----------|---------|--------|---------|--------|---------|---------|--------|---------|---------|
| つ (tsu) | さ (sa) | そ (so) | ひ (hi) | こ (ko) | み (mi) | も (mo) | ね (ne) | る (ru) | め (me) |

## Keyboard Layout

![HiraganaLaser Keyboard Layout](hiragana_laser_keymap.png)

## Troubleshooting

### **Input Source Not Appearing**
1. **Check file location:** Ensure `HiraganaLaser.keylayout` is in `~/Library/Keyboard Layouts/`
2. **Restart required:** Log out and back in, or restart your Mac
3. **Check permissions:** File should be readable (644 permissions)
4. **Manual activation:** Go to System Preferences > Keyboard > Input Sources to add manually

### **Characters Not Typing**
1. **Select correct input source:** Use the input source menu in your menu bar
2. **Test in different apps:** Try TextEdit, Terminal, or a web browser
3. **Check encoding:** Ensure the application supports UTF-8

### **Layout Validation Errors**
1. **"Key element with code X is repeated" error:**
   - This indicates duplicate key mappings in the layout file
   - Each key code should appear only once in the base mapping
   - Check the key code reference table for correct mappings
2. **"Keyboard layout was invalid" error:**
   - Verify the layout file is valid XML
   - Ensure all key codes correspond to physical QWERTY positions
   - Check for missing or incorrect key code mappings

## **Technical Specifications**

### **File Format & Structure**
- **Format**: XML-based .keylayout file (Apple KeyboardLayout.dtd v1.0 compliant)
- **Encoding**: UTF-8 (full Japanese character support)
- **Layout ID**: 16396 (Ukelele-generated, system-compatible)
- **Group**: 1 (keyboard group identifier)
- **Max Output**: 2 (supports multi-character output)
- **Structure**: ANSI layout (standard US keyboard compatibility)

### **Character Mapping Strategy**
- **Direct Mapping**: QWERTY → Hiragana (no Romaji conversion)
- **Complete Coverage**: All 46 basic Hiragana characters
- **Frequency Optimization**: High-frequency characters on easily accessible keys
- **Learning Progression**: Arranged for beginner-friendly learning
- **Control Preservation**: Essential keys (Enter, Tab, Backspace, Space) maintain functionality

### **System Requirements**
- **macOS**: 10.12+ (tested on macOS 15.7.1)
- **Keyboard Types**: ANSI, ISO (with minor adjustments)
- **Input Methods**: Direct character input, IME bypass
- **File Size**: ~7.5KB (optimized for performance)

### **Security & Compliance**
- **No External Dependencies**: Local file system only
- **No Network Access**: Completely offline operation
- **Apple DTD Compliance**: Follows official keyboard layout standards
- **Gatekeeper Compatible**: Works with macOS security features

## **Development Standards**

### **Enterprise-Grade Documentation**
- **Comprehensive Inline Comments**: Detailed XML documentation with technical specifications
- **Character Frequency Analysis**: Documented mapping strategies and frequency optimization
- **Technical Decision Rationale**: Clear explanations for architectural choices
- **Development History**: Complete change tracking and modification history

### **Code Quality Standards**
- **Apple DTD Compliance**: Full compliance with KeyboardLayout.dtd v1.0
- **UTF-8 Encoding**: Proper international character support
- **XML Structure**: Valid XML 1.1 document structure
- **Key Mapping Documentation**: Complete QWERTY→Hiragana mapping documentation

### **Testing & Validation**
- **Multi-Application Testing**: Validated across TextEdit, Terminal, Browser, Word
- **Character Accuracy**: Verified output for all 46 Hiragana characters
- **System Integration**: Tested input source switching and system compatibility
- **Security Validation**: Gatekeeper and security feature compatibility

### **Maintenance & Support**
- **Version Control**: Git-based development with branch protection
- **Documentation Updates**: Continuous documentation maintenance
- **Issue Tracking**: GitHub-based issue and feature tracking
- **Community Support**: Open-source development with community contributions

## License

This project is released under the CC0-1.0 license (Public Domain). See `LICENSE` file for details.

## File Structures

### **Simple Keyboard Layout (Working)**
```
~/Library/Keyboard Layouts/
└── HiraganaLaser.keylayout          # Direct keyboard layout file
```

**Installation:** Copy to `~/Library/Keyboard Layouts/` and restart
**Status:** ✅ **Working** - Ready for use and sharing
**Features:** Direct Hiragana input, basic functionality

### **Advanced Input Method Bundle (In Development)**
```
/Library/Input Methods/HiraganaLaser.app/
├── Contents/
│   ├── Info.plist                   # Main app configuration
│   ├── MacOS/
│   │   └── HiraganaLaser           # Main executable
│   └── PlugIns/
│       └── HiraganaLaser_Extension.appex/
│           └── Contents/
│               ├── Info.plist       # Extension config (Caps Lock support)
│               ├── MacOS/
│               │   └── HiraganaLaser_Extension
│               └── Resources/
│                   ├── HiraganaLaser.keylayout  # Keyboard layout
│                   └── Hiragana.tiff            # Icon
```

**Installation:** System-level bundle (requires admin privileges)
**Status:** 🔄 **In Development** - Caps Lock toggle not yet working
**Features:** Advanced input method, Caps Lock toggle (planned), system integration

## Files

- `HiraganaLaser.keylayout` - Main keyboard layout file
- `README.md` - This documentation
- `LICENSE` - CC0-1.0 license
- `DROP_x_MiTo_Laser_R2_Kobe_Hiragana_set.png` - Visual layout reference
- `Ukelele_Install_Menu.png` - Installation guide screenshot

---

**Status:** 
- ✅ **Simple Keyboard Layout** - Production ready with validated key codes and intuitive Shift mappings
- ✅ **Key Code Validation** - All duplicate key codes resolved, layout validates successfully
- ✅ **Intuitive Shift Mappings** - Small characters on same keys as large counterparts
- ✅ **Complete Small Character Set** - All essential small hiragana characters (ぁぃぅぇぉゃゅょっ)
- ✅ **Enterprise Documentation** - Complete key code reference and technical specifications
- 🔄 **Advanced Input Method Bundle** - In development (Caps Lock functionality not yet working)