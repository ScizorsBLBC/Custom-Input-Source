# Cursor AI Agent Rules Configuration

## Overview

This document outlines how to set up `.cursor/rules` to help Cursor AI agents follow best practices and work more effectively on this custom input source project.

## Directory Structure

```
.cursor/
└── rules/
    ├── documentation.mdc
    ├── keyboard-layout.mdc
    ├── security.mdc
    ├── testing.mdc
    └── git-workflow.mdc
```

## Rule Files

### 1. Documentation Rules (`documentation.mdc`)

```markdown
---
description: Enforce comprehensive documentation standards
globs: ["**/*.md", "**/*.keylayout"]
alwaysApply: true
---

# Documentation Standards for Custom Input Source Project

## Inline Documentation
- Add comprehensive XML comments to .keylayout files
- Document every key mapping with QWERTY->Hiragana explanation
- Include technical specifications and implementation details
- Follow industry standards for XML documentation

## README Documentation
- Always update README.md when adding new features
- Include installation instructions and troubleshooting
- Document known issues and workarounds
- Maintain comprehensive file listing

## Project Documentation
- Create PROJECT_HISTORY.md for development timeline
- Add DIAGNOSTIC_REPORT.md for technical analysis
- Include TROUBLESHOOTING.md for common issues
- Document all approaches tried and decisions made

## Code Comments
- Explain "why" not "what" in comments
- Document complex logic and business rules
- Include technical decision rationale
- Maintain consistency across all files
```

### 2. Keyboard Layout Rules (`keyboard-layout.mdc`)

```markdown
---
description: macOS keyboard layout development standards
globs: ["**/*.keylayout", "**/*.xml"]
alwaysApply: true
---

# Keyboard Layout Development Standards

## XML Structure
- Follow Apple's keyboard layout DTD requirements
- Use proper XML comment syntax
- Include comprehensive file headers
- Document all key mappings

## Character Mapping
- Map all QWERTY keys to appropriate Hiragana characters
- Include number row (0-9) mappings
- Document special characters and control keys
- Maintain logical character placement

## Technical Requirements
- Use UTF-8 encoding for Japanese characters
- Set unique layout ID (9999) to avoid conflicts
- Follow ANSI layout standards
- Include proper modifier map structure

## Security Considerations
- Address Gatekeeper security requirements
- Document code signing needs
- Include quarantine removal instructions
- Plan for notarization requirements
```

### 3. Security Rules (`security.mdc`)

```markdown
---
description: Security best practices for keyboard layouts
globs: ["**/*.keylayout", "**/*.md"]
alwaysApply: true
---

# Security Best Practices

## Gatekeeper Considerations
- Always check for quarantine attributes: `xattr -l filename`
- Document Gatekeeper bypass methods
- Include code signing requirements
- Plan for notarization process

## File Security
- Verify file permissions (644 for .keylayout files)
- Check for extended attributes
- Document security analysis in diagnostic reports
- Include security troubleshooting steps

## Installation Security
- Provide secure installation methods
- Document security workarounds
- Include verification steps
- Address system integrity protection (SIP)

## Code Signing
- Document developer certificate requirements
- Include signing process instructions
- Plan for Apple notarization
- Address distribution security
```

### 4. Testing Rules (`testing.mdc`)

```markdown
---
description: Testing and validation standards
globs: ["**/*.keylayout", "**/*.md"]
alwaysApply: false
---

# Testing and Validation Standards

## File Validation
- Validate XML structure: `xmllint --noout filename`
- Check property list format: `plutil -lint filename`
- Verify file encoding: `file filename`
- Test Gatekeeper compatibility: `spctl -a -v filename`

## Installation Testing
- Test in multiple applications (TextEdit, Terminal, Browser)
- Verify character output accuracy
- Test input source switching
- Validate system integration

## Documentation Testing
- Verify all links work correctly
- Test installation instructions
- Validate troubleshooting steps
- Check code examples

## System Compatibility
- Test on different macOS versions
- Verify with different keyboard types
- Test with various applications
- Validate security settings
```

### 5. Git Workflow Rules (`git-workflow.mdc`)

```markdown
---
description: Git workflow and version control standards
globs: ["**/*"]
alwaysApply: true
---

# Git Workflow Standards

## Commit Messages
- Use descriptive commit messages
- Include scope and impact information
- Reference issues and features
- Follow conventional commit format

## Branch Management
- Use main branch for stable releases
- Create feature branches for development
- Include pull request descriptions
- Maintain clean commit history

## File Organization
- Keep documentation files organized
- Maintain consistent naming conventions
- Include proper .gitignore rules
- Version control all project files

## Documentation Updates
- Update README.md with each significant change
- Maintain PROJECT_HISTORY.md
- Update troubleshooting guides
- Keep diagnostic reports current
```

## Implementation Guide

### 1. Create Directory Structure
```bash
mkdir -p .cursor/rules
```

### 2. Add Rule Files
Create each `.mdc` file with the content above, customized for your project needs.

### 3. Configure Rule Types
- **Always Apply**: Core project standards (documentation, security)
- **Auto Attached**: File-specific rules (keyboard-layout, testing)
- **Agent Requested**: Optional rules for specific contexts
- **Manual**: Rules invoked only when needed

### 4. Test Rules
- Restart Cursor after adding rules
- Test with different file types
- Verify rule application
- Adjust rules as needed

## Best Practices

### Rule Design
- **Keep rules focused** on specific aspects
- **Use clear descriptions** for AI understanding
- **Apply appropriate glob patterns** for file targeting
- **Organize hierarchically** for complex projects

### Maintenance
- **Review rules regularly** for relevance
- **Update rules** as project evolves
- **Test rule effectiveness** with AI interactions
- **Document rule changes** in project history

### Troubleshooting
- **Verify file extensions** (.mdc required)
- **Check frontmatter syntax** (YAML format)
- **Review glob patterns** for accuracy
- **Restart Cursor** after changes

## Project-Specific Considerations

### Custom Input Source Focus
- Emphasize macOS keyboard layout standards
- Include Japanese character encoding requirements
- Address Gatekeeper security challenges
- Document installation troubleshooting

### Documentation Requirements
- Comprehensive inline documentation
- Complete project history tracking
- Detailed diagnostic analysis
- Thorough troubleshooting guides

### Security Considerations
- Gatekeeper bypass methods
- Code signing requirements
- Quarantine attribute handling
- System integration security

This rules system ensures Cursor AI agents work effectively within the project's specific requirements and maintain high standards for documentation, security, and development practices.
