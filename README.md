# Document Processing Pipeline

A comprehensive document processing pipeline built in Jupyter Notebook that transforms scanned documents, PDFs, and images into fully searchable, metadata-rich, and forensically verified outputs. Designed for document digitization, forensic analysis, and accessibility enhancement.

## Features

### 📄 **Format Support**
- **Input Formats**: PDF, TIFF, JPEG, PNG, ZIP archives
- **Output Format**: Searchable PDF with embedded OCR text layer
- Automatic format normalization to ensure consistent pipeline processing

### 🔍 **Advanced Document Analysis**
- **High-Precision OCR**: Uses Tesseract with 300 DPI conversion for accuracy
- **Deep Metadata Extraction**: Extracts PDF metadata, XMP data, EXIF tags, and file signatures
- **Cryptographic Hashing**: SHA-256 hash calculation for document integrity verification
- **Forensic Support**: Hex signature extraction and comprehensive metadata logging

### 👁️ **Human-in-the-Loop Verification**
- Interactive GUI for reviewing and correcting OCR-extracted text
- Page-by-page verification interface
- Quality control before final document finalization

### 🔒 **Searchability & Security**
- Embeds invisible OCR text layer into PDFs for full-text search capability
- Maintains document appearance while adding searchable content
- Preserves original file integrity with validation checksums

### 📦 **Batch Processing**
- Process multiple documents in a single session
- Support for ZIP archive extraction and processing
- Organized export with metadata alongside processed documents
- Automated workspace cleanup for batch resets

## Pipeline Workflow

```
1. Environment Setup          → Install dependencies (Tesseract, OCR tools, Python libraries)
2. File Upload               → Upload documents (PDF, TIFF, images, or ZIP files)
3. Archive Extraction        → Automatically extract ZIP files and validate contents
4. Format Normalization      → Convert all formats (TIFF, images) to standardized PDF
5. Metadata & Hash Extraction → Extract deep metadata and calculate document hash
6. High-Precision OCR        → Convert pages to 300 DPI images and extract text
7. Human Verification       → Review and correct OCR text via interactive interface
8. Embed Hidden Text Layer  → Inject verified OCR text as invisible searchable layer
9. Final Export             → Package processed PDFs with metadata and provide download
```

## Installation & Setup

### Prerequisites
- **Python 3.x** (Google Colab recommended)
- **Tesseract OCR**: System-level dependency
- **Supporting Libraries**: `pytesseract`, `pdf2image`, `PyMuPDF`, `pikepdf`, `pdfplumber`, `Pillow`, `exifread`

### Running in Google Colab

1. **Open the Notebook**  
   Click the "Open in Colab" badge or visit the repository's `Document_Processing_Pipeline.ipynb`

2. **Run Environment Setup**  
   Execute the first code cell to install all system and Python dependencies

3. **Follow Sequential Cells**  
   Run cells in order from top to bottom (they are numbered 1–9)

### Running Locally

```bash
# Clone the repository
git clone https://github.com/carlymariec/document_processing_pipeline.git
cd document_processing_pipeline

# Install dependencies
pip install pytesseract pdf2image PyMuPDF pikepdf pdfplumber Pillow exifread ipywidgets

# Install Tesseract (macOS)
brew install tesseract

# Install Tesseract (Ubuntu/Debian)
sudo apt-get install tesseract-ocr libtesseract-dev libleptonica-dev

# Launch Jupyter Notebook
jupyter notebook Document_Processing_Pipeline.ipynb
```

## Usage

### Step-by-Step Workflow

#### 1. **Upload Documents**
- Click the **Upload Documents** button
- Select multiple files: PDFs, TIFFs, images (JPG/PNG), or ZIP archives
- Files are hashed and logged immediately for integrity tracking

#### 2. **Archive Extraction** (if applicable)
- ZIP files are automatically extracted
- Valid documents (PDF, TIFF, JPG, PNG) are identified and processed
- Invalid files are skipped with error logging

#### 3. **Format Normalization**
- Images and TIFF files are converted to PDF format
- PDFs remain unchanged
- Enables unified processing downstream

#### 4. **Metadata & Hash Collection**
- Extracts PDF metadata, XMP data, and EXIF information
- Calculates SHA-256 hash for each document
- Logs all metadata to `*_metadata.txt` files

#### 5. **OCR Extraction**
- Converts PDF pages to 300 DPI high-resolution images
- Uses Tesseract to extract text with high precision
- Progress shown page-by-page

#### 6. **Human Verification** *(Optional but Recommended)*
- Review extracted OCR text page-by-page
- Edit text directly in the interface if needed
- Mark pages as approved or corrected

#### 7. **Embed Searchable Text**
- Injects verified OCR text as an invisible layer in the PDF
- Text is hidden but fully searchable and selectable
- Document appearance remains unchanged

#### 8. **Export Results**
- Click **Download Processed Files** to get a ZIP archive
- Archive contains:
  - Searchable PDFs (`*_searchable.pdf`)
  - Metadata logs with hashes (`*_metadata.txt`)
  - Complete audit trail

#### 9. **Cleanup**
- Run the workspace erasure function to prepare for the next batch
- Removes all temporary and processed files
- Resets the registry for fresh processing

## Output Files

| File Type | Description |
|-----------|-------------|
| `*_searchable.pdf` | Final processed PDF with embedded OCR text layer |
| `*_metadata.txt` | Comprehensive metadata log including hash values |
| `*_normalized.pdf` | Intermediate PDF after format normalization |
| `Forensic_Processed_Docs.zip` | Complete batch export ready for download |

## Key Functions

### Core Processing Functions

- **`calculate_hash(file_path, algorithm='sha256')`**  
  Computes cryptographic hash for document integrity verification

- **`extract_metadata(file_path)`**  
  Extracts deep metadata, EXIF, hex signatures, and file headers

- **`normalize_to_pdf(registry)`**  
  Converts all image formats to standardized PDFs

- **`perform_ocr(registry)`**  
  Runs high-precision Tesseract OCR at 300 DPI resolution

- **`embed_hidden_text(registry)`**  
  Injects invisible searchable OCR text layer into PDFs

- **`export_results(registry)`**  
  Packages final outputs and metadata for batch download

- **`erase_workspace()`**  
  Clears all files and resets for new batch processing

## Use Cases

- **Document Digitization**: Convert paper documents to searchable digital format
- **Forensic Analysis**: Extract and verify metadata for legal investigations
- **Accessibility Enhancement**: Make scanned documents searchable for all users
- **Records Management**: Batch process and organize archived documents
- **Research**: Extract text from historical documents while preserving originals

## Technical Details

### OCR Settings
- **Resolution**: 300 DPI (high precision)
- **Engine**: Tesseract OCR with English language model
- **Output**: Character-level text extraction

### Hash Algorithm
- **Default**: SHA-256
- **Purpose**: Verify document integrity and detect tampering

### PDF Optimization
- Processed through `pikepdf` for structural validation and optimization
- Maintains compatibility with standard PDF readers

## Supported Libraries

| Library | Purpose |
|---------|---------|
| `pytesseract` | Tesseract OCR interface |
| `pdf2image` | PDF to image conversion |
| `PyMuPDF (fitz)` | PDF creation and manipulation |
| `pikepdf` | PDF validation and optimization |
| `pdfplumber` | PDF text extraction (future enhancement) |
| `Pillow` | Image processing |
| `exifread` | EXIF metadata extraction |
| `ipywidgets` | Interactive UI components |

## Limitations & Considerations

- **OCR Accuracy**: Depends on document quality; handwritten text may not extract well
- **Processing Time**: Large documents or high batch sizes take proportional time
- **Google Colab Quotas**: Free tier has storage and runtime limits
- **File Size**: Individual files should be under 100MB for optimal performance
- **Language Support**: Currently configured for English; other languages require Tesseract model installation

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Tesseract not found | Ensure system-level installation completed in first cell |
| OCR quality poor | Check PDF quality; verify 300 DPI conversion ran successfully |
| Memory errors on large batches | Process fewer files per batch; clear workspace between runs |
| Metadata extraction fails | File may be corrupted; try re-uploading |
| Searchable PDF not working | Verify hidden text embedding completed; check PDF with different reader |

## Future Enhancements

- [ ] Multi-language OCR support
- [ ] Machine learning-based document classification
- [ ] Advanced text segmentation and layout analysis
- [ ] Batch API endpoint for programmatic access
- [ ] Direct integration with cloud storage services
- [ ] Performance optimization for very large batches

## License

This project is open source. Please check the repository for the specific license.

## Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request with detailed descriptions

## Support & Issues

For bugs, feature requests, or questions:
- Open an issue on the [GitHub repository](https://github.com/carlymariec/document_processing_pipeline/issues)
- Include error logs and sample files when applicable

## Citation

If you use this pipeline in your research or work, please cite:

```
Document Processing Pipeline by Carly Marie C.
https://github.com/carlymariec/document_processing_pipeline
```

---

**Last Updated**: June 2026  
**Python Version**: 3.x  
**Primary Environment**: Google Colab  
**Notebook Version**: Latest (Document_Processing_Pipeline.ipynb)
