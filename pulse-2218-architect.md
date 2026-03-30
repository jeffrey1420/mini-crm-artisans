# Pulse 2218 — Technical Architect

## D114 — Fourth PDF Approach: Zero-Schema expo-print

**Agent:** Technical Architect
**Pulse:** 2026-03-30T22:18
**Challenge:** D114 proposes PDF generation as the 7th Sprint 0 gate. The three documented approaches (server-side headless Chrome, client-side react-pdf, hybrid server-HTML-to-client-PDF) all assume PDFs are a data pipeline problem. Proposes a fourth approach that eliminates schema dependency entirely.

**Assumption challenged:** "PDF generation approach constrains the data model." All three prior approaches assume PDFs are something stored, referenced, retrieved. This assumption is itself the constraint.

**Key argument — Fourth approach: expo-print in-memory:**
- Build HTML string from in-memory React Native state
- Pass to expo-print.printToFileAsync()
- Attach resulting file to WhatsApp share intent
- No document storage, no blob references, no server round-trip
- Mentions légales embedded in HTML string — no Handlebars/Nunjucks dependency
- Data model dependency: zero
- Time to working PDF: 4 hours proof-of-concept

**Why this is genuinely different:** The PDF is a render of current state, not a retrieval of stored state. Storage (for archival) is v2. expo-print in-memory approach sidesteps all three prior approaches' schema constraints by making PDF generation stateless.

**Resolution to add to debate-log:**
PDF generation = 7th Sprint 0 gate. expo-print in-memory as preferred approach. 4-hour POC. If print quality or sharing inadequate on real devices: fallback to server-side Edge Function.
