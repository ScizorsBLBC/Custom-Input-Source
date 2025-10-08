# HiraganaLaser Input Method Bundle

## **Overview**

This is the development version of the HiraganaLaser input method bundle. This structure represents the advanced input method implementation that provides Caps Lock toggle functionality and full system integration.

## **Bundle Structure**

```
HiraganaLaser-InputMethod.app/
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
│                   └── HiraganaLaser.keylayout  # Keyboard layout
```

## **Installation**

To install this input method bundle:

1. **Copy to system directory:**
   ```bash
   sudo cp -r HiraganaLaser-InputMethod.app /Library/Input\ Methods/HiraganaLaser.app
   ```

2. **Set proper ownership:**
   ```bash
   sudo chown -R root:wheel /Library/Input\ Methods/HiraganaLaser.app
   ```

3. **Restart input method services:**
   ```bash
   sudo killall -HUP TextInputMenuAgent
   sudo killall -HUP TextInputSwitcher
   ```

4. **Add to enabled input sources:**
   ```bash
   defaults write com.apple.HIToolbox AppleEnabledInputSources -array-add '{InputSourceKind = "Non Keyboard Input Method"; "Bundle ID" = "com.scizors.inputmethod.HiraganaLaser";}'
   ```

## **Features**

- **Caps Lock Toggle**: `TICapsLockLanguageSwitchCapable = true`
- **Input Method Integration**: Full system integration
- **Component Input Modes**: Proper input mode configuration
- **NSExtension Support**: Input method services integration

## **Status**

🔄 **In Development** - Caps Lock functionality not yet working

## **Development Notes**

This bundle structure follows Apple's input method conventions and should enable the Caps Lock toggle option in System Settings when properly installed and configured.
