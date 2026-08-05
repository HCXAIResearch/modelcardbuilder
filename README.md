# Model Card Generator (Deployer Edition)

| Field | Value |
|---|---|
| Title | Model Card Generator — Deployer Edition |
| Document Reference | HCXAI-prj04-001 |
| Version | 1.0 |
| Status | Released |
| Owner | HCXAIResearch (https://hcxairesearch.org/) |
| Audience | AI governance leads, compliance and procurement teams, deployment owners |
| Standards Reference | ISO/IEC 42001:2023; ISO/IEC 42005:2025; NIST AI RMF 1.0; EU AI Act (Regulation 2024/1689); OECD AI Principles; Model Cards for Model Reporting (Mitchell et al., 2019) |
| License | See LICENSE |
| Project Link | https://hcxairesearch.github.io/modelcardbuilder/ |

A single-file, browser-based tool that produces a model card for an AI system **from the perspective of the organisation deploying it**. You fill in what the provider's public documentation tells you, add your own deployment context and controls, and export a clean card as PDF, HTML or Markdown.

Eight form sections, a live preview, three export formats. No backend, no build step, no telemetry.

---

## Why this exists

The original model card (Mitchell et al., 2019) was written for the party that trained the model. A deployer is not that party. When an organisation adopts a frontier model through an API, it holds none of the training internals, none of the raw evaluation harness, and no privileged view of the safety work — it holds the vendor's published documentation and its own deployment.

Most model-card templates ignore that asymmetry and ask the deployer for fields it cannot honestly complete. The result is either blank sections or borrowed claims presented as first-hand knowledge.

This tool takes the deployer's position as the design premise. Two distinctions run through it and are enforced by the section structure:

| Distinction | Consequence for the card |
| --- | --- |
| What the **vendor states** vs. what **you know** | Capability, performance, limitation and safety fields are labelled as vendor-stated and paired with a source-documentation trail. They are attributions, not assertions |
| What the **model is** vs. what **you do with it** | Intended use, environment, oversight, guardrails and monitoring are your fields. They describe the deployment, which is the part you actually control and can be held to |

Everything the tool asks for is something a deploying organisation can obtain from public documentation or state about its own operation.

---

## What is in it

The card is assembled from eight sections. Fields left blank are omitted from the rendered card, so a partial card stays clean.

| # | Section | What it captures | Perspective |
| --- | --- | --- | --- |
| 1 | Identification | Model name, provider, version, modality, deployment status, who prepared the card, date | Factual |
| 2 | Source documentation | The vendor material the card is built on — title and reference for each. The provenance trail | Vendor |
| 3 | Intended use (as deployed) | Your deployment purpose, intended users in your context, out-of-scope and prohibited uses | Deployer |
| 4 | Vendor-stated capabilities & performance | Capability summary and reported benchmark results, attributed to the provider | Vendor |
| 5 | Limitations & risks | Known limitations, bias and fairness notes, safety considerations, as documented | Vendor |
| 6 | Deployment context & mitigations | Environment and integration, human oversight, guardrails, monitoring and feedback | Deployer |
| 7 | Governance tags | NIST AI RMF functions addressed; EU AI Act risk classification; governance rationale | Deployer |
| 8 | Contact | Where questions about the card go | Factual |

The rendered card leads with governance, so the classification and framework tags sit above the detail rather than buried at the end.

---

## Running it

Open `model-card-generator.html` in any modern browser. That is the whole installation procedure.

To host it, drop the file anywhere that serves static content — SharePoint document library, internal wiki, S3 bucket, GitHub Pages. It has no server dependency and no same-origin requirement.

The only external requests are Google Fonts. If your environment blocks them, the tool degrades to the declared fallbacks (system sans-serif) with no loss of function. To make it fully self-contained, remove the two `<link rel="preconnect">` tags and the stylesheet `<link>` in `<head>`.

---

## Files

| File | Purpose |
| --- | --- |
| `model-card-generator.html` | The tool. Self-contained: markup, CSS, form logic and export logic in one file |
| `README.md` | This document |
| `USER_MANUAL.md` | Field-by-field guidance, worked example, export notes, customisation |

---

## Design and branding

Branded to the HCXAIResearch identity, using the house pairing rather than a departure. Tokens are declared once in `:root` and nothing downstream hard-codes a colour.

| Token | Value | Role |
|---|---|---|
| `--navy` | `#1B2A4A` | Card masthead, dark panels, headings |
| `--teal` | `#0E7C7B` | Primary accent — buttons, section rules, active state |
| `--teal-deep` | `#124E52` | Logomark, section headers on light surfaces |
| `--teal-tint` | `#E6F4F4` | NIST tag fill, section-rule tint |
| `--ink` | `#111827` | Body text |
| `--muted` | `#5b6572` | Secondary text, hints, footer |
| `--border` | `#e4e8ec` | Hairlines and card borders |
| `--bg` | `#f5f7f9` | Page stock |

EU AI Act risk tags carry their own semantic colours — red (Prohibited), amber (High-risk), blue (Limited risk), green (Minimal risk), grey (Not classified) — deliberately outside the brand palette so a classification is never mistaken for decoration.

**Typography.** Poppins for the wordmark and the card title; Inter for the interface and body. This is the HCXAI house pairing. Unlike the Geneva module, the subject here carries no institutional register that would justify a serif, so the house faces stand.

**Signature device.** The rendered card mirrors the on-screen preview exactly: a navy masthead with a teal base rule, a governance band of colour-coded tags, then field groups under teal-ruled section heads. The bracket-and-figure logomark closes the card footer beside the preparer and date.

**Emblem.** The HCXAI bracket-and-figure logomark, inline SVG. The wordmark is rebuilt in markup (HCX in ink, AI in teal, Research in light) rather than shipped as an image, so it stays crisp at any export size.

Matching social assets (1080×1080 and 1200×630) are maintained alongside the tool for release announcements.

---

## Technical notes

- Vanilla JavaScript, no framework, no bundler. There is no separate data model: the form is the source of truth, and the renderer reads the DOM on every `input` and `change` event.
- **No browser storage.** State is in memory only. A reload clears the form, by design — the tool builds one card at a time and does not track a library. Export before you close the tab.
- Source documentation and benchmark results are **repeatable rows**; add or remove as many as the documentation supports.
- Exports:
  - **HTML** and **Markdown** are `Blob` downloads and always work, including inside a sandboxed iframe.
  - **Print / PDF** uses the browser's native print dialog with a print stylesheet that hides the editor and prints the card alone. In a normal browser tab this produces a clean PDF; note that `window.print()` can be blocked inside sandboxed iframes, so open the file directly to print.
- The export filename is derived from the model name (slugified), e.g. `gemini-1-0-pro-model-card.md`.
- **Load sample** fills a worked deployer-side example; **Clear** resets to an empty card with today's date.

---

## Scope limits

Read these before circulating a generated card.

1. **Deployer perspective throughout.** The card documents what a deploying organisation can source from public documentation or state about its own operation. It is not the provider's own model card and does not reproduce training internals or privileged safety results.
2. **Attribution, not verification.** The tool records what you enter. It does not check vendor claims, validate benchmark figures, or confirm that a cited document says what the card says it does. Accuracy of the vendor-stated fields is yours to establish.
3. **Not legal or compliance advice.** The EU AI Act classification and NIST AI RMF tags are your own governance reading recorded on the card, not an attestation of conformance. Where a deployment decision turns on either, take qualified advice.
4. **A card, not a control.** A completed card documents a position; it does not enforce one. The mitigations section describes controls you have implemented elsewhere.
5. **No persistence.** Nothing is stored between sessions. There is no audit trail unless you export and file the output yourself.

---

## Roadmap

| Item | Note |
|---|---|
| Control mapping | Governance tags extended to `ISO/IEC 42001` Annex A controls and `ISO/IEC 42005` assessment structure, as selectable tags |
| OECD tag | OECD AI Principles alongside the NIST and EU AI Act tags |
| Markdown front matter | Optional YAML front matter on the Markdown export (model, provider, version, risk, date) for docs-repo and static-site use |
| JSON snapshot | Export and re-import a card as JSON, consistent with the SharePoint versioning pattern used across the HCXAI toolkit |
| Card library | Optional multi-card mode, moving beyond the current one-at-a-time flow |
| True OOXML export | A genuine `.docx` writer for automated document pipelines, replacing the current Markdown route where required |

---

## Changelog

| Version | Change |
|---|---|
| 1.0 | Initial release. Eight deployer-focused sections, live preview, PDF/HTML/Markdown export, NIST AI RMF and EU AI Act governance tags, HCXAI house palette and logomark |
| 0.2 | Export set changed from Word to Markdown; export now PDF / HTML / Markdown |
| 0.1 | First build. Form, preview and PDF/HTML/Word export |

---

*HCXAIResearch · Human Centered Explainable AI (Governance) · `HCXAI-prj04-001` v1.0*
