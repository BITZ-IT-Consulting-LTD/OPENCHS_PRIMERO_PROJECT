# Folder reorganisation record

**Date:** 26 October 2026  
**Scope:** Folder organisation and navigation repair; requirements, approvals and commercial dates unchanged.

All 100 pre-existing files were retained. Current working files are grouped into eight numbered folders, with `README.md` and `inception.md` at the top level. The misspelled `temeplate forms` folder and active folder name ending in a space were replaced by `04_templates/` and the meeting folders. Nested `docs/docs/platform/reference` content was flattened under technical references.

## Preservation and navigation

- The original scope PDF, meeting PDFs and PPTX decks were moved without changing their bytes.
- The five transcript formats were given consistent names and labelled unreviewed; transcript bytes were preserved.
- The current Excel workbook and its archived output copy were preserved byte for byte.
- The earlier dated snapshot was moved intact under `08_archive/previous_versions/`, retaining its original structure and references.
- One identical extra Session 1 PDF and the earlier identical workbook output copy were retained in archive folders; neither was deleted.
- Working Markdown relative links and three Word documents’ local hyperlink targets were updated for the new locations. Word document body XML, formatting, embedded assets and visible text were unchanged.
- Original source paths quoted in historical narratives or technical examples remain attribution, rather than current navigation. Use the move manifest when tracing these paths.
- Empty former folders were removed only after their files had been relocated. Local metadata and Python cache files were preserved separately and ignored as local generated files.

## Verification

The [move manifest](FOLDER_MOVE_MANIFEST_2026-10-26.json) contains every old/new path, original size and before/after SHA-256 values. The accompanying folder validation record checks that every file remains present, unchanged binary source files retain their hashes, current local Markdown and Word hyperlinks resolve, the inventory totals remain 7 Resolved / 53 Pending / 11 Deferred, and Office archives remain readable.

No files were deleted, source PDFs/decks rewritten, transcript accuracy asserted, external messages sent, Git commits created or live integration tests performed.
