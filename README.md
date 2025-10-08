# HiraganaLaser - Custom Japanese Input Source

A custom macOS keyboard layout that enables direct typing of Hiragana characters on a QWERTY keyboard, designed for use with custom mechanical keyboards. It uses the DROP x MiTo Laser R2 GMK 'Kobe' Hiragana legends keycaps or another set that has the same layout.

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