# Documents (문서)

이 디렉토리에 PDF 문서들을 추가하세요.
Add PDF documents to this directory.

## Recommended Files (권장 파일):

### Conference Materials
- `krcc2026_poster.pdf` - KRcC 2026 conference poster
- `krcc2026_platform_poster.pdf` - Related platform poster

### Thesis Materials
- `thesis_abstract.pdf` - M.S. thesis abstract (English)
- `thesis_abstract_kr.pdf` - M.S. thesis abstract (Korean)

### Technical Documentation
- `technical_specifications.pdf` - Sensor specifications
- `user_manual.pdf` - Installation and operation guide

## File Specifications:
- **Format:** PDF
- **Max Size:** 50MB
- **Recommended:** 2-10MB (compress if needed)

## PDF Compression:
```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook \
   -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
```

See `/MEDIA_UPLOAD_GUIDE.md` for detailed instructions.
