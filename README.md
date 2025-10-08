# HiraganaLaser - Custom Japanese Input Source

A custom macOS keyboard layout that enables direct typing of Hiragana characters on a QWERTY keyboard, designed for use with custom mechanical keyboards.

## Overview

This project provides a working macOS input source that maps QWERTY keys directly to Hiragana characters, enabling efficient Japanese text input without IME conversion.

## Features

✅ **Complete Hiragana Character Set** - All 46 basic Hiragana characters mapped  
✅ **Number Row Support** - Numbers 0-9 mapped to Hiragana characters  
✅ **Proper Backspace** - Correct backspace functionality  
✅ **macOS Integration** - Works with System Preferences Input Sources  
✅ **UTF-8 Encoding** - Proper Japanese character support  

## Installation

### **Method 1: Direct Installation (Recommended)**

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

### **Method 2: Ukelele Bundle (Alternative)**

If you prefer a bundle format:

1. **Download Ukelele** from [software.sil.org/ukelele](https://software.sil.org/ukelele/)
2. **Open the layout:** File → Open → Select `HiraganaLaser.keylayout`
3. **Set keyboard name:** File → Set Keyboard Name → "HiraganaLaser"
4. **Save as bundle:** File → Save As Bundle → Save as `HiraganaLaser.bundle`
5. **Install:** Copy the bundle to `~/Library/Keyboard Layouts/`
6. **Restart** and add to Input Sources as above

## Key Mapping

### **Number Row (Top Row)**
| Key | Hiragana | Key | Hiragana | Key | Hiragana | Key | Hiragana | Key | Hiragana |
|-----|----------|-----|----------|-----|----------|-----|----------|-----|----------|
| 0 | ち (chi) | 1 | と (to) | 2 | し (shi) | 3 | は (ha) | 4 | く (ku) |
| 5 | き (ki) | 6 | つ (tsu) | 7 | さ (sa) | 8 | そ (so) | 9 | ひ (hi) |

### **Main Letter Rows**

#### **Top Row (Q-P)**
| Q | W | E | R | T | Y | U | I | O | P |
|---|----|----|----|----|----|----|----|----|----|
| こ (ko) | て (te) | あ (a) | ら (ra) | た (ta) | や (ya) | う (u) | い (i) | お (o) | ん (n) |

#### **Home Row (A-L)**
| A | S | D | F | G | H | J | K | L |
|---|----|----|----|----|----|----|----|----|
| あ (a) | す (su) | で (de) | ふ (fu) | が (ga) | は (ha) | ま (ma) | か (ka) | る (ru) |

#### **Bottom Row (Z-M)**
| Z | X | C | V | B | N | M |
|---|----|----|----|----|----|----|
| ざ (za) | く (ku) | せ (se) | べ (be) | ば (ba) | な (na) | も (mo) |

### **Special Keys**
- **Space**: Space (unchanged)
- **Enter**: Enter (unchanged)  
- **Backspace**: Backspace (unchanged)
- **Tab**: Tab (unchanged)
- **Brackets**: 「」 (Japanese quotation marks)

## Visual Layout

![HiraganaLaser Keyboard Layout](Laser%20Keymap%20Image.png)

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

### **Backspace Issues**
- The current version has fixed backspace functionality
- If issues persist, reinstall the layout file

## Technical Details

- **File Format:** XML-based .keylayout file
- **Encoding:** UTF-8 for Japanese character support
- **Layout ID:** 9999 (custom, avoids system conflicts)
- **Compatibility:** macOS 10.12+ (tested on macOS 15.7.1)
- **File Size:** ~7.5KB

## Development

This project uses industry-standard practices:
- Comprehensive inline XML documentation
- Proper macOS keyboard layout DTD compliance
- UTF-8 encoding for international characters
- Clear QWERTY→Hiragana mapping documentation

## License

This project is released under the CC0-1.0 license (Public Domain). See `LICENSE` file for details.

## Files

- `HiraganaLaser.keylayout` - Main keyboard layout file
- `README.md` - This documentation
- `LICENSE` - CC0-1.0 license
- `Laser Keymap Image.png` - Visual layout reference

---

**Status:** ✅ **Working** - Ready for use and sharing