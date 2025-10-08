# Troubleshooting Guide

## Common Issues and Solutions

### Installation Issues

#### Issue: Layout doesn't appear in Input Sources
**Symptoms:**
- Copied .keylayout file but can't find it in System Preferences
- Layout doesn't show up in the list of available input sources

**Solutions:**
1. **Restart Required**: macOS requires a restart or logout/login after adding keyboard layouts
2. **File Location**: Ensure file is in `~/Library/Keyboard Layouts/` (not `/Library/Keyboard Layouts/`)
3. **File Permissions**: Check that the file has proper read permissions
4. **XML Validation**: Verify the .keylayout file has valid XML structure

#### Issue: Layout appears but doesn't work
**Symptoms:**
- Layout shows up in Input Sources but typing produces wrong characters
- No output when typing

**Solutions:**
1. **Input Source Selection**: Make sure "HiraganaLaser" is actually selected in the input source menu
2. **Application Compatibility**: Some applications may not support custom keyboard layouts
3. **System Restart**: Try a full system restart after installation
4. **Layout ID Conflict**: Check if another layout is using the same ID (9999)

### Character Output Issues

#### Issue: Wrong characters appearing
**Symptoms:**
- Typing produces unexpected characters
- Some keys work, others don't

**Solutions:**
1. **Key Mapping Verification**: Check the key mapping table in README.md
2. **Application Testing**: Test in different applications (TextEdit, Terminal, etc.)
3. **Input Source Verification**: Ensure the correct layout is selected
4. **System Language**: Check if system language settings are interfering

#### Issue: No output from certain keys
**Symptoms:**
- Some keys produce no output
- Specific characters missing

**Solutions:**
1. **Key Code Verification**: Check if key codes are correctly mapped in the XML
2. **Unicode Encoding**: Verify UTF-8 encoding is properly set
3. **Application Support**: Some applications may not support all Unicode characters
4. **Layout Validation**: Use a text editor to verify the .keylayout file structure

### System Integration Issues

#### Issue: Layout doesn't persist after restart
**Symptoms:**
- Layout works initially but disappears after restart
- Need to reinstall frequently

**Solutions:**
1. **File Permissions**: Ensure proper ownership and permissions
2. **System Integrity**: Check if system security settings are interfering
3. **Backup**: Keep a backup of the working .keylayout file
4. **Installation Method**: Try copying to `/Library/Keyboard Layouts/` instead

#### Issue: Conflicts with other input methods
**Symptoms:**
- Layout interferes with other keyboard layouts
- Switching between layouts causes issues

**Solutions:**
1. **Input Source Management**: Use System Preferences to manage input sources
2. **Layout Priority**: Set preferred input sources in System Preferences
3. **Conflict Resolution**: Remove conflicting layouts if necessary
4. **Testing**: Test with minimal input sources enabled

### Development and Customization Issues

#### Issue: Want to modify the layout
**Symptoms:**
- Need to change character mappings
- Want to add new characters

**Solutions:**
1. **XML Editing**: Edit the .keylayout file with a text editor
2. **Key Code Reference**: Use macOS key code documentation
3. **Unicode Characters**: Find Unicode codes for desired characters
4. **Testing**: Test changes in a text editor before system-wide installation

#### Issue: Adding modifier key combinations
**Symptoms:**
- Want to use Shift/Option for additional characters
- Need multiple character sets

**Solutions:**
1. **Modifier Maps**: Add new modifierMap entries in the XML
2. **Key Map Sets**: Create additional keyMap entries for different modifier states
3. **Documentation**: Update README.md with new key combinations
4. **Testing**: Thoroughly test all modifier combinations

## Diagnostic Steps

### Step 1: Verify Installation
```bash
# Check if file exists in correct location
ls -la ~/Library/Keyboard\ Layouts/HiraganaLaser.keylayout

# Check file permissions
ls -la ~/Library/Keyboard\ Layouts/
```

### Step 2: Test in Different Applications
1. **TextEdit**: Basic text editing
2. **Terminal**: Command line interface
3. **Web Browser**: Online text input
4. **Word Processor**: Advanced text editing

### Step 3: Check System Logs
```bash
# Check for keyboard-related errors
log show --predicate 'subsystem == "com.apple.keyboard"' --last 1h

# Check for input method errors
log show --predicate 'subsystem == "com.apple.inputmethod"' --last 1h
```

### Step 4: Validate XML Structure
```bash
# Check XML validity (requires xmllint)
xmllint --noout ~/Library/Keyboard\ Layouts/HiraganaLaser.keylayout
```

## Advanced Troubleshooting

### System-Level Issues
- **SIP (System Integrity Protection)**: May interfere with system-level keyboard layouts
- **Gatekeeper**: Security settings may block custom layouts
- **FileVault**: Encryption may affect layout loading

### Application-Specific Issues
- **Sandboxed Applications**: Some apps may not support custom layouts
- **Security Software**: Antivirus or security tools may interfere
- **Input Method Conflicts**: Other input methods may take precedence

### Performance Issues
- **Layout Loading**: Large layouts may load slowly
- **Memory Usage**: Complex layouts may use more memory
- **Switching Speed**: Multiple layouts may slow switching

## Getting Help

### Documentation References
- **README.md**: Complete installation and usage guide
- **PROJECT_HISTORY.md**: Development history and technical details
- **Key Mapping Tables**: Complete character mapping reference

### System Information to Include
When reporting issues, include:
- macOS version
- Application where issue occurs
- Exact steps to reproduce
- Error messages (if any)
- System configuration details

### Testing Checklist
Before reporting issues, verify:
- [ ] File is in correct location
- [ ] System has been restarted
- [ ] Layout is selected in Input Sources
- [ ] Tested in multiple applications
- [ ] Checked system logs for errors
- [ ] Verified XML structure is valid
