# Security Policy

## Overview

This document outlines the security practices and guidelines for the Document Processing Pipeline project. **The pipeline is designed to process sensitive documents and user data locally in Google Colab or on personal machines. NO user data or personal documents are ever stored in this public repository.**

## Data Protection Principles

### ✅ What This Repository Contains
- Source code (Jupyter Notebook with processing logic)
- Configuration and setup instructions
- Documentation and usage guides
- Dependencies and requirements
- **NO user documents, processed files, or personal data**

### ❌ What Will NEVER Be Stored Here
- User-uploaded PDF, TIFF, or image files
- Processed or searchable PDFs
- Metadata extraction logs containing document information
- User credentials, API keys, or authentication tokens
- Google Colab session data or credentials
- Temporary working files or caches

## Security Features

### 🔒 Repository-Level Security

1. **Comprehensive `.gitignore`**
   - All document formats (`*.pdf`, `*.tiff`, `*.jpg`, `*.png`, `*.zip`) are ignored
   - Processing output directories are excluded
   - User data folders are blocked from commits
   - Temporary and cache files are automatically excluded

2. **Secrets Protection**
   - `.env` files and environment variables excluded
   - API keys and credentials never stored
   - Google Colab authentication files ignored
   - No hardcoded sensitive data in notebooks

3. **File Type Blocking**
   - No binary document files tracked
   - No processed output files committed
   - No system or OS files included
   - No backup or temporary files stored

### 🛡️ Code-Level Security

The notebook implements security best practices:

```python
# ✅ Hash Calculation - Verifies document integrity
def calculate_hash(file_path, algorithm='sha256'):
    """Cryptographic hash for authenticity verification"""
    # Uses SHA-256 for strong cryptographic verification
    # No data is persisted beyond the session

# ✅ Metadata Extraction - Local processing only
def extract_metadata(file_path):
    """Extracts metadata locally without transmitting data"""
    # All processing happens in user's environment
    # No data uploaded to external services

# ✅ File Upload - Local storage only
def handle_upload(change):
    """Handles file uploads to local Colab storage"""
    # Files saved to local workspace, not persisted
    # Deleted at session end or via cleanup function
```

## Usage Security Guidelines

### For Google Colab Users

1. **Sensitive Documents**
   - Upload documents only during your active session
   - Documents are stored in temporary Colab storage
   - Auto-deleted when session disconnects
   - No data persists between sessions

2. **Download Results**
   - Download processed files to your local machine immediately
   - Delete the ZIP archive from Colab after download
   - Use the `erase_workspace()` function to clear all files

3. **Authentication**
   - Colab authentication is session-specific
   - Never share your session URL
   - Don't paste sensitive credentials into cells

### For Local Execution

1. **Workspace Setup**
   ```bash
   # Create isolated directory for document processing
   mkdir -p ~/document_processing/{uploads,processed,exports}
   cd ~/document_processing
   
   # Ensure .gitignore is in place
   git clone https://github.com/carlymariec/document_processing_pipeline.git
   cd document_processing_pipeline
   ```

2. **Local Data Handling**
   - Keep documents in separate directories outside git repo
   - Store uploads and exports in `uploads/` and `processed_docs/` (git-ignored)
   - All directories are in `.gitignore` - won't be committed

3. **Cleanup**
   ```bash
   # After processing, remove all user documents
   rm -rf uploads/ processed_docs/ Forensic_Processed_Docs/
   # Or use the notebook's erase_workspace() function
   ```

## Protected Information Categories

### 🚫 Never Committed
- **Personal Documents**: PDFs, scanned papers, images
- **Metadata Files**: Hash logs with document information
- **Archive Files**: ZIP files containing user content
- **Credentials**: API keys, tokens, authentication data
- **Cache Files**: Temporary processing files
- **System Files**: `.DS_Store`, Thumbs.db, etc.

### ✅ Always Safe
- **Source Code**: Notebook logic and processing functions
- **Documentation**: README, SECURITY policy, setup guides
- **Configuration**: Public settings and dependencies
- **License & Contributing**: Open source guidelines

## Pre-Commit Verification Checklist

**Before pushing to GitHub, verify:**

- [ ] No `*.pdf` files in tracked files
- [ ] No `*.zip` archives in version control
- [ ] No `.env` or credentials files committed
- [ ] No `_metadata.txt` files with sensitive data
- [ ] No `processed_docs/` or `uploads/` directories
- [ ] `.gitignore` is current and comprehensive

```bash
# Check what will be committed
git status

# Verify .gitignore is working
git check-ignore -v uploads/ processed_docs/ *.pdf *.zip

# See what files Git is tracking (should NOT include documents)
git ls-files
```

## Accidental Data Exposure Prevention

### If You Accidentally Commit Sensitive Data:

1. **Immediate Action**
   ```bash
   # Remove from git history (be careful!)
   git rm --cached <filename>
   git commit --amend
   git push --force-with-lease
   ```

2. **Notify GitHub**
   - GitHub automatically removes sensitive data from caches
   - Consider updating any exposed credentials

3. **Update .gitignore**
   - Add patterns to prevent future accidents

## Regular Security Audits

1. **Before Each Release**
   - Verify no document files in repo
   - Check for hardcoded credentials
   - Review recent commits for sensitive data
   - Test `.gitignore` rules

2. **Community Contributions**
   - PR reviews check for security issues
   - Maintain `.gitignore` integrity
   - Document security practices

## Security Reporting

🔐 **Report security vulnerabilities responsibly:**

- **Do NOT** open public GitHub issues for security concerns
- Contact the maintainer privately via GitHub security advisories
- Provide details of the vulnerability and reproduction steps
- Allow time for patching before public disclosure

## Legal & Compliance

- This project is for **local document processing only**
- Users are responsible for complying with document confidentiality laws
- No data is transmitted to external services without user knowledge
- Users must have permission to process uploaded documents

## Dependencies Security

All Python dependencies are from PyPI and can be audited:

- `pytesseract` - Open source OCR interface
- `pdf2image` - PDF conversion library
- `PyMuPDF` - PDF manipulation
- `pikepdf` - PDF validation
- `pdfplumber` - PDF text extraction
- `Pillow` - Image processing
- `exifread` - EXIF data extraction
- `ipywidgets` - Interactive UI

**Security Note**: Keep dependencies updated via:
```bash
pip install --upgrade pytesseract pdf2image PyMuPDF pikepdf pdfplumber Pillow exifread
```

## Best Practices for Users

### ✅ DO:
- Process documents in isolated environments
- Download and backup results to personal storage
- Delete files from cloud sessions after processing
- Use `.gitignore` rules locally
- Review exported files before sharing
- Enable 2FA on GitHub account

### ❌ DON'T:
- Commit document files to the repository
- Share Colab session URLs with others
- Store sensitive documents in uploads/ that's tracked by Git
- Hardcode credentials in notebooks
- Skip workspace cleanup
- Upload documents from unauthorized sources

## Maintenance & Updates

This security policy is reviewed and updated regularly. Users are notified of:
- Security patches
- `.gitignore` changes
- New data protection features
- Vulnerable dependency updates

---

**Last Updated**: June 2026  
**Policy Version**: 1.0  
**Repository**: https://github.com/carlymariec/document_processing_pipeline

**For questions about security, please open a GitHub Discussion or contact the maintainer.**
