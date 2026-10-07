# Transcripts & Docs

Store meeting recordings, Word transcripts, and supporting documents here.

## How to Add Your Meeting Transcript

1. **Save the Word document** in this folder with format: `[Meeting Type] Transcript - [Date].docx`
   - Example: `EIS Transcript - 07-30-2026.docx`

2. **Link from Meeting Notes:** In the corresponding meeting note (in `Meeting Notes/` folder), update the metadata:
   ```yaml
   transcript: "Transcripts & Docs/EIS Transcript - 07-30-2026.docx"
   ```

3. **Reference in body:** Add a section like:
   ```markdown
   ## Full Transcript
   📎 [Full Meeting Transcript](Transcripts & Docs/EIS Transcript - 07-30-2026.docx)
   ```

## Asset Organization

```
Transcripts & Docs/
├── [Meeting Type] Transcript - [Date].docx
├── [Meeting Type] Recording - [Date].mp4
└── [Supporting Document].pdf
```

---

**Tip:** Markdown notes go in `Meeting Notes/`; binary files (Word docs, PDFs, recordings) stay here.
