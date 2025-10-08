# Custom Input Source for Japanese Hiragana

A custom macOS keyboard layout that allows direct typing of Hiragana characters on a QWERTY keyboard, designed for use with custom mechanical keyboards.

## Project Overview

This project creates a custom input source for macOS that maps QWERTY keys directly to Hiragana characters, enabling efficient Japanese text input without the need for IME (Input Method Editor) conversion.

## Current Status

✅ **Completed:**
- Basic Hiragana keyboard layout (`HiraganaLaser.keylayout`)
- Direct character mapping for all basic Hiragana characters
- Proper XML structure following macOS keyboard layout standards

🔄 **In Progress:**
- Testing and refinement of key mappings
- Documentation and installation instructions

📋 **Planned:**
- Katakana layout variant
- Dakuon/Han-dakuon support (voiced consonants)
- Small character support (っ, ゃ, ゅ, ょ, etc.)
- Modifier key combinations for additional characters

## Files

- `HiraganaLaser.keylayout` - The main keyboard layout file
- `README.md` - This documentation file
- `PROJECT_HISTORY.md` - Complete development history and technical details
- `TROUBLESHOOTING.md` - Troubleshooting guide for common issues
- `DIAGNOSTIC_REPORT.md` - Technical analysis of installation issues
- `DOCUMENTATION_STANDARDS.md` - Inline documentation standards
- `CURSOR_AI_RULES.md` - Cursor AI agent configuration and best practices
- `LICENSE` - CC0-1.0 license file

## Installation

### **Method 1: Direct Installation (Current)**
1. Copy `HiraganaLaser.keylayout` to `~/Library/Keyboard Layouts/`
2. Restart your Mac or log out and back in
3. Go to System Preferences > Keyboard > Input Sources
4. Click the "+" button and add "HiraganaLaser" from the list
5. Select the layout from the input source menu

### **Method 2: Ukelele Bundle Creation (Recommended)**
For proper macOS integration, use Ukelele to create a bundle:

#### **Step 1: Download and Install Ukelele**
1. Download Ukelele from [software.sil.org/ukelele](https://software.sil.org/ukelele/)
2. Install the application in your Applications folder

#### **Step 2: Create Bundle from Existing Layout**
1. **Open Ukelele**
2. **File → Open** → Select `HiraganaLaser.keylayout`
3. **File → Set Keyboard Name** → Enter "HiraganaLaser"
4. **File → Save As Bundle** → Save as `HiraganaLaser.bundle`

#### **Step 3: Install the Bundle**
1. Copy `HiraganaLaser.bundle` to `~/Library/Keyboard Layouts/`
2. Restart your Mac
3. Go to System Preferences > Keyboard > Input Sources
4. Click "+" → Find "HiraganaLaser" → Add

#### **Step 4: Verify Installation**
- Check Input Sources list for "HiraganaLaser"
- Test character output in TextEdit
- Verify all key mappings work correctly

### ⚠️ **Known Installation Issues**

**🚨 CRITICAL ISSUE**: Gatekeeper Security Blocking
**Root Cause**: macOS Gatekeeper rejecting unsigned keyboard layout file
**Status**: **PRIMARY BLOCKING ISSUE**

**Diagnostic Findings:**
- ✅ File exists in correct location with proper permissions
- ✅ XML structure is valid
- 🚨 **Gatekeeper blocking**: `rejected - source=no usable signature`
- ⚠️ Property list validation fails (macOS expects specific format)
- ⚠️ Layout not automatically enabled in system

**Immediate Workarounds:**
1. **🚨 Bypass Gatekeeper**: 
   ```bash
   xattr -d com.apple.quarantine ~/Library/Keyboard\ Layouts/HiraganaLaser.keylayout
   ```
2. **Right-click → Open**: Bypasses Gatekeeper for single use
3. **Manual Activation**: Manually add layout in System Preferences
4. **System Restart**: Full restart may be required

**Long-term Solutions:**
- **Code Signing**: Sign the .keylayout file with developer certificate
- **Format Conversion**: Convert to proper macOS keyboard layout format
- **Alternative Location**: Try `/Library/Keyboard Layouts/` (system-wide)

**See [DIAGNOSTIC_REPORT.md](DIAGNOSTIC_REPORT.md)** for complete technical analysis.

### **Ukelele Troubleshooting**

**Issue**: Bundle doesn't appear in Input Sources
**Solutions**:
1. **Verify Bundle Creation**: Ensure Ukelele saved as `.bundle` format
2. **Check File Location**: Bundle must be in `~/Library/Keyboard Layouts/`
3. **Restart Required**: Full system restart after installation
4. **Permissions**: Ensure bundle has proper read permissions

**Issue**: Ukelele can't open .keylayout file
**Solutions**:
1. **File Format**: Ensure file is valid XML with proper DOCTYPE
2. **Encoding**: Check UTF-8 encoding is correct
3. **Structure**: Verify XML structure follows Apple DTD
4. **Alternative**: Create new layout in Ukelele and copy mappings

**Issue**: Characters not displaying correctly
**Solutions**:
1. **Font Support**: Ensure application supports Japanese characters
2. **Input Source**: Verify correct layout is selected
3. **Application Testing**: Test in TextEdit, Terminal, Browser
4. **System Restart**: May require restart for full integration

## Key Mapping

The layout maps QWERTY keys to Hiragana characters as follows:

![HiraganaLaser Keyboard Layout](Laser%20Keymap%20Image.png)

*Visual representation of the HiraganaLaser keyboard layout showing direct Hiragana character mappings*

### Number Row (Top Row)
| QWERTY Key | Hiragana | QWERTY Key | Hiragana |
|------------|----------|------------|----------|
| 0 | ち (chi) | 5 | き (ki) |
| 1 | と (to) | 6 | つ (tsu) |
| 2 | し (shi) | 7 | さ (sa) |
| 3 | は (ha) | 8 | そ (so) |
| 4 | く (ku) | 9 | ひ (hi) |

### Main Letter Rows
| QWERTY Key | Hiragana | QWERTY Key | Hiragana |
|------------|----------|------------|----------|
| Q | ち (chi) | A | あ (a) |
| W | と (to) | S | す (su) |
| E | し (shi) | D | て (te) |
| R | は (ha) | F | ふ (fu) |
| T | く (ku) | G | か (ka) |
| Y | き (ki) | H | ひ (hi) |
| U | つ (tsu) | J | ん (n) |
| I | さ (sa) | K | ぬ (nu) |
| O | そ (so) | L | る (ru) |
| P | ひ (hi) | ; | れ (re) |
| [ | こ (ko) | ' | け (ke) |
| ] | た (ta) | \ | の (no) |
| A | あ (a) | Z | や (ya) |
| S | す (su) | X | ゆ (yu) |
| D | て (te) | C | よ (yo) |
| F | ふ (fu) | V | わ (wa) |
| G | か (ka) | B | ほ (ho) |
| H | ひ (hi) | N | め (me) |
| J | ん (n) | M | も (mo) |
| K | ぬ (nu) | , | ね (ne) |
| L | る (ru) | . | み (mi) |
| ; | れ (re) | / | ろ (ro) |
| ' | け (ke) | | | |
| \ | の (no) | | | |

## Technical Details

- **Format**: macOS Keyboard Layout (.keylayout)
- **Encoding**: UTF-8
- **Layout ID**: 9999 (custom)
- **Group**: 0
- **Modifier Support**: Basic (no shift/option combinations yet)

## Development Notes

The layout uses standard macOS keyboard layout XML format with:
- Unique keyboard ID (9999) to avoid conflicts
- ANSI key mapping for standard US keyboard
- Direct character output without IME processing
- Proper XML structure following Apple's DTD

## Future Enhancements

1. **Katakana Support**: Create a parallel Katakana layout
2. **Dakuon/Han-dakuon**: Add support for voiced consonants (が, ざ, だ, etc.)
3. **Small Characters**: Support for っ, ゃ, ゅ, ょ, etc.
4. **Modifier Keys**: Use Shift/Option for additional character sets
5. **Installation Script**: Automated installation and setup

## License

This project is released under the CC0-1.0 license (Public Domain).

## Documentation

- **[PROJECT_HISTORY.md](PROJECT_HISTORY.md)** - Complete development history, approaches tried, and technical decisions
- **[TROUBLESHOOTING.md](TROUBLESHOOTING.md)** - Common issues and solutions for installation and usage
- **[CURSOR_AI_RULES.md](CURSOR_AI_RULES.md)** - Cursor AI agent configuration and best practices

## Cursor AI Agent Configuration

This project includes comprehensive `.cursor/rules` configuration to help Cursor AI agents work more effectively:

### **Rule Categories**
- **Documentation Standards**: Comprehensive inline documentation requirements
- **Keyboard Layout Development**: macOS keyboard layout best practices
- **Security Best Practices**: Gatekeeper and code signing considerations
- **Testing Standards**: File validation and installation testing
- **Git Workflow**: Version control and commit standards

### **Implementation**
```bash
# Create Cursor rules directory
mkdir -p .cursor/rules

# Add rule files (see CURSOR_AI_RULES.md for complete setup)
# Each rule file should be .mdc format with frontmatter metadata
```

### **Benefits**
- ✅ **Consistent Documentation**: AI agents follow project documentation standards
- ✅ **Security Awareness**: Automatic consideration of Gatekeeper and security issues
- ✅ **Quality Standards**: Enforced testing and validation practices
- ✅ **Project Context**: AI agents understand custom input source requirements

**See [CURSOR_AI_RULES.md](CURSOR_AI_RULES.md)** for complete configuration guide.

## Contributing

This is a personal project for custom mechanical keyboard use, but contributions and suggestions are welcome!
