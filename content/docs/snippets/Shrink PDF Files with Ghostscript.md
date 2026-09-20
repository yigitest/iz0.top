# Shrink PDF Files with Ghostscript

Compress and reduce the file size of a PDF using Ghostscript (`gs`). This optimizes documents for email attachments or web distribution.

## Prerequisites

- Ghostscript (`gs`) installed on your system.

## Command

Run the following command to compress `<input.pdf>` using the `/ebook` preset (150 dpi):

```bash
gs \
  -sDEVICE=pdfwrite \
  -dCompatibilityLevel=1.4 \
  -dPDFSETTINGS=/ebook \
  -dNOPAUSE \
  -dQUIET \
  -dBATCH \
  -sOutputFile=<output.pdf> \
  <input.pdf>
```

### PDF Quality Presets

Adjust `-dPDFSETTINGS` to control resolution and output size:

- `/screen`: Lowest quality, smallest size (72 dpi).
- `/ebook`: Medium quality, balanced size (150 dpi, default recommendation).
- `/printer`: High quality (300 dpi).
- `/prepress`: Highest quality with full color preservation (300 dpi).

## Verify

Compare the file sizes of the original and compressed documents:

```bash
ls -lh <input.pdf> <output.pdf>
```

> [!WARNING]
> Do not use the same filename for `<sOutputFile>` and `<input.pdf>`. Overwriting the input file directly can corrupt the PDF.
