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

## Installation

1. Copy `HiraganaLaser.keylayout` to `~/Library/Keyboard Layouts/`
2. Restart your Mac or log out and back in
3. Go to System Preferences > Keyboard > Input Sources
4. Click the "+" button and add "HiraganaLaser" from the list
5. Select the layout from the input source menu

## Key Mapping

The layout maps QWERTY keys to Hiragana characters as follows:

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

## Contributing

This is a personal project for custom mechanical keyboard use, but contributions and suggestions are welcome!
