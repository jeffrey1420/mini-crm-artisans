# Debate: WhatsApp Sharing Architecture for Sprint 0

**Architect:** Technical Architect
**Date:** 2026-03-30
**Status:** RESOLVED

---

## The Question

How should WhatsApp sharing work in Sprint 0 for a French artisan sending a devis to a client? Two approaches compete:

- **Approach A — PDF Attachment:** Generate PDF server-side, open native share sheet, user selects WhatsApp, PDF attaches
- **Approach B — WhatsApp-Native Message:** In-app compose with rich preview, deep link to view devis online, PDF as secondary download

The question matters for Sprint 0 because WhatsApp is the primary sharing channel (D42) and PDF generation was pushed to Sprint 1b (D2). These decisions are in tension.

---

## Approach A — PDF Attachment

**Arguments:**

1. **No WhatsApp Business API required.** Native iOS/Android share sheet works without any WhatsApp-specific integration. User taps "Share" → selects WhatsApp → PDF attaches → sends. This is the path of least resistance.

2. **Matches actual artisan behavior today.** What does Marc do when he needs to send a devis now? He WhatsApp a photo of a handwritten note, or an Excel screenshot, or a PDF from his computer. Giving him a PDF in WhatsApp is an upgrade, not a behavior change.

3. **PDF is self-contained.** The client receives a document they can print, forward, and archive regardless of their phone/computer/email setup. This is important for French B2B where clients may be on different devices and platforms.

4. **PDF generation is Sprint 1b work.** D2 already scheduled PDF generation for Sprint 1b (Days 6-10). If Sprint 0 uses share sheet + PDF attachment, the flow works immediately after Sprint 1b ships.

5. **Risk:** PDF rendering across Android devices is non-trivial. HTML-to-PDF on mobile (via html-to-pdf libraries or webview capture) is fragile. But this risk is already priced into Sprint 1b scope.

---

## Approach B — WhatsApp-Native Message

**Arguments:**

1. **Lower friction for the sender.** No PDF to generate, no attachment to load. The message is composed in-app with a preview card, sent with one tap.

2. **Works without PDF generation in Sprint 0.** If the devis data is stored in Supabase, a deep link (`minicrm://devis/123`) can open the full devis in the recipient's phone. No PDF generation needed for sharing — only for archival.

3. **WhatsApp Business API has message template restrictions.** If using WhatsApp Business API to send messages directly, the message content must comply with WhatsApp's template rules. A template-based approach limits what you can say in the message. This constrains the product's ability to include custom messaging.

4. **The "native message" approach is actually how most French artisans communicate.** They already WhatsApp clients. Adding a structured message with a link is a smaller behavior change than asking them to attach PDFs.

5. **Deep link tracking.** A `minicrm://` link can track when the recipient opened the devis, for how long, etc. PDF attachments give no read receipts. For the €29 tier's financial snapshot, read tracking has value.

---

## Technical Considerations

**On WhatsApp Business API:**
- Sending messages directly via WhatsApp Business API requires pre-approved message templates. For a devis being sent from an artisan to their client, this would need to be a transactional template — not a marketing template. Getting a transactional template approved for "new devis notification" takes 1-2 weeks and requires a business account.
- The native share sheet (Approach A) bypasses this entirely — the artisan's personal WhatsApp sends the message, no API approval needed.
- Direct API-based sending is NOT viable for Sprint 0.

**On PDF generation complexity:**
- Server-side PDF generation (Fastify edge function or Supabase Edge Function) is straightforward: take HTML template, render to PDF, return URL.
- Client-side PDF (React Native webview capture) is unreliable across Android versions.
- Sprint 1b (Days 6-10) already includes PDF generation. The question is whether it's needed for Sprint 0 sharing.
- If Sprint 0 ships with Approach A, the share sheet works with a placeholder PDF or a simple text attachment until Sprint 1b delivers proper PDF.

**On deep links:**
- `minicrm://` deep links require universal link/app link configuration on both iOS and Android.
- For iOS: Associated Domains (apple-app-site-association file on the landing page domain)
- For Android: App Links verification via Digital Asset Links
- Sprint 0 timeline (5 days) may not accommodate universal link setup + testing on both platforms.
- Deep links can be a Sprint 1 addition.

**On the "rich preview" card:**
- WhatsApp generates its own preview card from the URL meta tags when a link is shared.
- If the deep link points to a Supabase-hosted preview page, WhatsApp will auto-generate a preview card with the devis summary.
- This requires a simple landing page for each devis with OG tags — technically trivial, but an additional Sprint 0 deliverable.

---

## Sprint 0 Recommendation

**Ship Approach A (PDF Attachment) in Sprint 0, plan Approach B as Sprint 1.**

**Why:**
1. PDF via native share sheet requires zero WhatsApp-specific API work. Works Day 1.
2. PDF generation is already Sprint 1b scoped — a placeholder PDF (even a simple text attachment) can stand in until proper PDF is ready.
3. WhatsApp Business API for direct sending is not viable in Sprint 0 — template approval takes weeks.
4. The deep link / rich preview approach (Approach B) is the right long-term direction, but needs universal link setup + preview page + testing — belongs in Sprint 1.

**Sprint 0 scope for sharing:**
- Native share sheet integration (React Native `Share` API)
- Placeholder attachment (simple text or generated PDF if html-to-pdf library available in <2h)
- WhatsApp pre-selected in share sheet if available
- Supabase Storage for PDF hosting once generated

**Sprint 1 additions:**
- Server-side PDF generation (html-to-pdf via Edge Function or Puppeteer)
- Universal/app deep links for devis preview
- Rich preview card (OG tags on preview page)
- Read receipts for €29 tier (track when recipient opened)

**What NOT to do in Sprint 0:**
- Do not attempt WhatsApp Business API direct sending — template approval alone takes longer than Sprint 0
- Do not build a custom in-app WhatsApp composer — this duplicates the native share sheet
- Do not defer native sharing to wait for perfect PDF — ship with text attachment, upgrade to PDF in Sprint 1b

---

## Resolution

**RESOLVED — Approach A for Sprint 0, Approach B for Sprint 1.**

| Sprint | Sharing deliverable |
|--------|-------------------|
| Sprint 0 | Native share sheet + placeholder attachment (text or basic PDF) |
| Sprint 1b | Server-side PDF generation with mentions légales |
| Sprint 1 (later) | Universal deep links + WhatsApp preview card |
| Sprint 1.1 | Read receipts for €29 tier |

The WhatsApp sharing architecture is not a Sprint 0 blocker. Native share sheet ships with Sprint 0. PDF generation and deep links are Sprint 1 work.