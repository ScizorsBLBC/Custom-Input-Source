# Test Layouts Directory

## **Purpose**

This directory contains experimental and test versions of the ひらがな keyboard layout for development and testing purposes.

## **Directory Structure**

```
test-layouts/
├── README.md                           # This file
├── Hiragana_backup.keylayout          # Backup of production layout
├── Hiragana_test1.keylayout           # Test version 1
├── Hiragana_test2.keylayout           # Test version 2
└── [additional test files]            # Future test versions
```

## **Testing Best Practices**

### **Before Testing**
1. **Backup production layout**:
   ```bash
   cp ~/Library/Keyboard\ Layouts/Hiragana.keylayout test-layouts/Hiragana_backup.keylayout
   ```

2. **Document test purpose** in filename and comments

3. **Verify system state**:
   - Check current input sources
   - Verify Karabiner Elements status
   - Note any active modifications

### **During Testing**
1. **Test incrementally** - one change at a time
2. **Document results** - what works, what doesn't
3. **Test with multiple applications** - TextEdit, Terminal, Browser
4. **Test input source switching** - ABC ↔ ひらがな

### **After Testing**
1. **Restore production layout** if needed:
   ```bash
   cp test-layouts/Hiragana_backup.keylayout ~/Library/Keyboard\ Layouts/Hiragana.keylayout
   ```

2. **Document findings** in DEVELOPMENT_README.md

3. **Clean up** - remove failed test files

## **Test File Naming Convention**

- `Hiragana_backup.keylayout` - Production backup
- `Hiragana_test[N].keylayout` - Test version N
- `Hiragana_[feature].keylayout` - Feature-specific test
- `Hiragana_[issue].keylayout` - Issue-specific test

## **Testing Checklist**

### **Basic Functionality**
- [ ] Layout loads without errors
- [ ] Input source appears in System Settings
- [ ] Can switch to input source
- [ ] Basic Hiragana characters work
- [ ] Shift combinations work
- [ ] Control keys preserved

### **Advanced Features**
- [ ] Combining characters work
- [ ] Small characters work
- [ ] Long vowel sound works
- [ ] All 46 basic characters work
- [ ] No duplicate key codes

### **Integration Testing**
- [ ] Works with Karabiner Elements
- [ ] Works with USB hub setup
- [ ] Works with macro pad
- [ ] Works in different applications
- [ ] No system conflicts

## **Common Issues**

### **Layout Not Loading**
- Check XML syntax
- Verify key code format
- Check for duplicate key codes
- Verify layout ID uniqueness

### **Characters Not Typing**
- Check input source selection
- Verify key code mappings
- Test in different applications
- Check system permissions

### **System Conflicts**
- Disable Karabiner Elements temporarily
- Check for conflicting input sources
- Verify system settings
- Test with clean user account

## **Recovery Procedures**

### **If Layout Breaks System**
1. **Switch to ABC input source** immediately
2. **Remove broken layout**:
   ```bash
   rm ~/Library/Keyboard\ Layouts/Hiragana.keylayout
   ```
3. **Restart system** or log out/in
4. **Restore from backup**:
   ```bash
   cp test-layouts/Hiragana_backup.keylayout ~/Library/Keyboard\ Layouts/Hiragana.keylayout
   ```

### **If Input Source Disappears**
1. **Check file location** and permissions
2. **Restart input method services**:
   ```bash
   sudo killall -HUP TextInputMenuAgent
   sudo killall -HUP TextInputSwitcher
   ```
3. **Re-add to input sources** in System Settings

## **Development Notes**

- **Always test on working-branch** before merging to main
- **Document all changes** in commit messages
- **Use version control** for all test files
- **Keep backups** of working versions
- **Test with real hardware** when possible

---

**Last Updated**: 2025-01-27  
**Version**: 1.0  
**Status**: Active Development
