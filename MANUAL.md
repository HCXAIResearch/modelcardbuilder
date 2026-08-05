---
title: "Model Card Generator (Deployer Edition) — User Manual"
document_ref: HCXAI-prj04-001-M
version: 1.0
status: Released
owner: HCXAIResearch
applies_to: model-card-generator.html v1.0
audience: AI governance leads, deployment owners, compliance and procurement teams, self-directed users
---

# User Manual

Everything needed to complete, export and adapt a deployer's model card. Section 1 covers the interface, section 2 the ways to use it, section 3 field-by-field guidance, section 4 exports, section 5 a worked example, section 6 customisation.

---

## Contents

1. [Getting started](#1-getting-started)
2. [Ways to use it](#2-ways-to-use-it)
3. [Field-by-field guidance](#3-field-by-field-guidance)
4. [Exporting](#4-exporting)
5. [Worked example](#5-worked-example)
6. [Customisation](#6-customisation)
7. [Accessibility](#7-accessibility)
8. [Troubleshooting](#8-troubleshooting)

---

## 1. Getting started

Open `model-card-generator.html` in a browser. There is nothing to install.

### The interface

| Element | Behaviour |
| --- | --- |
| Header | HCXAI logomark and wordmark, the label **Model Card Generator**, and the export controls |
| Editor | Left column. Eight numbered sections of form fields. Scrolls independently |
| Preview | Right column. The live card. Every keystroke updates it. Empty fields do not appear |
| Repeatable rows | **Source documentation** and **benchmark results** each carry an **+ Add** button and a **×** to remove a row |
| Export controls | **Load sample**, **Clear**, **HTML**, **Markdown**, **Print / PDF**, left to right in the header |

On a screen narrower than about 940 px the two columns stack, editor above preview.

### Two things to know before you start

**Nothing is stored.** A reload clears the form. Export the card — or at minimum keep the tab open — until you have the file you need. See [section 4](#4-exporting).

**The card omits what you leave blank.** There is no need to fill every field. A card with three sections completed renders as a clean three-section card, not a form full of gaps. Complete what the documentation supports and what your deployment warrants.

---

## 2. Ways to use it

### Full documentation pass — recommended

Work top to bottom with the vendor's documentation open beside you.

| Order | Section | Note |
| --- | --- | --- |
| 1 | Identification | Fill first; the model name drives the export filename |
| 2 | Source documentation | List the vendor material before you quote it. Everything downstream is attributed to these sources |
| 3 | Intended use | Your deployment, in your words. The first genuinely deployer-owned section |
| 4–5 | Capabilities, Limitations | Transcribe from the vendor docs. Keep it to what they actually state |
| 6 | Deployment context | Your environment, oversight and guardrails |
| 7 | Governance tags | Classify last, once the rest of the card gives you the basis to |

Budget twenty to thirty minutes with the documentation to hand.

### Rapid triage card

Sections 1, 3 and 7 only — identification, intended use, and the governance classification. Produces a one-screen card that answers *what is it, what are we doing with it, and how have we classified it* for an intake or registry entry. Fill the rest later.

### Governance-tag pass

Open an existing exported card, then use the tool to redo sections 1 and 7 when a classification changes — a new EU AI Act reading, or a NIST function newly addressed — and re-export. Faster than editing the exported file by hand.

---

## 3. Field-by-field guidance

The recurring discipline across every section: **vendor-sourced fields are attributions, deployer fields are commitments.** Write the first as "the provider states…", write the second as something you would stand behind in review.

### 1 · Identification

Factual header. **Deployment status** is a state, not a quality claim — *Under evaluation*, *Approved for deployment*, *Deployed — monitored*, *Restricted use*, *Retired*. **Card prepared by** defaults to HCXAIResearch; change it to the accountable team. The date defaults to today.

**Tip:** put the specific version and date in **Model version** (e.g. `1.0 (Feb 2024)`), not just a family name. A card that does not say which version it describes ages badly.

### 2 · Source documentation

This is the section that makes the rest of the card honest. Each row is a title and a reference. List the model card or technical report, the acceptable-use or prohibited-use policy, the terms of service, and any benchmark page you draw on.

**Watch:** if a claim in section 4 or 5 has no corresponding source here, either add the source or soften the claim. An unsourced vendor claim on a deployer's card is the failure mode this tool exists to prevent.

### 3 · Intended use (as deployed)

The first deployer-owned section. **Purpose** is your use, not the model's general capability. **Intended users** is who in your organisation interacts with it. **Out-of-scope and prohibited uses** should carry both your own exclusions and any the vendor prohibits — cite their policy for the latter.

**Discussion prompt for a review:** if the purpose field could be copied onto a card for any model from the same vendor, it is too generic to be useful. Name the workflow.

### 4 · Vendor-stated capabilities & performance

Transcribe, do not editorialise. The capability summary is the provider's account of what the model does well. Benchmark rows are name and reported result — add a row noting that figures are vendor-reported and not independently verified.

**Anticipate:** the temptation to add capabilities you have observed in your own use. Keep those in section 6 if they concern your deployment; this section is the vendor's account only.

### 5 · Limitations & risks

The most consequential vendor-sourced section, and the one most often left thin. Pull known limitations, bias and fairness notes, and safety considerations from the documentation. Where the vendor reports dangerous-capability or content-safety evaluations relevant to your use, summarise them here with the source in section 2.

**Line worth using in review:** a limitations section shorter than the capabilities section usually means the capabilities came from marketing and the limitations from nowhere.

### 6 · Deployment context & mitigations

Entirely yours, and the part a reviewer or auditor can actually hold you to. **Environment** covers how and where the model runs, what data reaches it, and who has access. **Human oversight** names where a person reviews or can override. **Guardrails** are the controls you apply — filtering, prompt constraints, rate limits, disclaimers. **Monitoring** is what you log and how issues surface.

**Watch:** describe controls that exist, not controls you intend. If oversight is planned but not yet in place, say so — a card that overstates the mitigations is worse than one that admits the gap.

### 7 · Governance tags

**NIST AI RMF functions** — tick the functions this deployment addresses (Govern, Map, Measure, Manage). Ticking a function is a claim that you do the corresponding work, recorded elsewhere.

**EU AI Act risk classification** — your assessment of the deployed use case, not the model in the abstract. The tag colours by level so it reads at a glance. Leave it *Not classified* until you have a basis.

**Governance rationale** — one paragraph on why the classification holds, which obligations it triggers, who owns it, and when it is next reviewed. This is what turns a coloured tag into a defensible record.

### 8 · Contact

Where questions about the card go. A role or shared mailbox outlasts an individual.

---

## 4. Exporting

Three formats, chosen from the header. All render the same card; they differ in destination.

| Format | Control | Use it for | Mechanism |
| --- | --- | --- | --- |
| PDF | **Print / PDF** | A fixed record for a governance file or evidence pack | Browser print dialog; a print stylesheet hides the editor and prints the card alone. Choose *Save as PDF* as the destination |
| HTML | **HTML** | A self-contained page for a wiki, portal or SharePoint library | `Blob` download of a standalone file with the card's styles inlined |
| Markdown | **Markdown** | A docs repository, static-site generator, or plain-text record | `Blob` download; headings, tables for benchmarks, code-span governance tags, autolinked sources |

The filename derives from the model name, e.g. `gemini-1-0-pro-model-card.pdf`.

**On PDF and sandboxed environments.** Print / PDF relies on the browser's native `window.print()`. In a normal browser tab this is the cleanest route to a PDF. Inside a sandboxed iframe — some embedded previews and portals — `window.print()` may be blocked, which is a known constraint across the HCXAI toolkit. If the button does nothing, open `model-card-generator.html` directly in a tab, or use the **HTML** export and print that. **HTML** and **Markdown** are `Blob` downloads and are never affected.

**Filing the card.** Consistent with the versioning approach used across the toolkit: export, then attach the file to the system of record — a SharePoint library entry, a model registry row, or the deployment's governance folder. There is no backend to query, and the tool keeps no copy.

---

## 5. Worked example

**Load sample** populates a complete deployer-side card for *Gemini 1.0 Pro* as adopted through an API for internal drafting. It is illustrative, not authoritative — the figures and readings are for demonstration. Use it to see the intended register, then clear it.

| Section | Sample content, abridged |
| --- | --- |
| Identification | Gemini 1.0 Pro · Google · v1.0 (Feb 2024) · text + image input, text output · *Deployed — monitored* |
| Source documentation | Gemini technical report; the model card appendix; the provider's prohibited-use policy |
| Intended use | Drafting and summarising internal research notes; output is always a first draft, never a published deliverable. Internal staff only |
| Capabilities | General text reasoning, summarisation, multilingual and image understanding, per vendor |
| Benchmarks | MMLU 79.13%; GSM8K 86.5%; plus a row flagging figures as vendor-reported |
| Limitations | Hallucinations; English-centric performance; limited long-horizon reasoning |
| Deployment context | API access inside internal tooling; no customer PII sent; named reviewer signs off; content filtering, rate limits and an AI-generated disclaimer |
| Governance | EU AI Act: *Limited risk*; NIST AI RMF: Govern, Measure, Manage; rationale citing mandatory human review and no automated decision-making |

The register to copy: vendor sections attributed and sourced, deployer sections specific and committal, and a governance rationale that explains the classification rather than merely asserting it.

---

## 6. Customisation

All markup, styles and logic sit in the one file. The changes below are the ones most likely to be wanted.

### Adding, removing or renaming a field

Fields live in the `<form id="form">` block, grouped by `<fieldset>`. Each input has an `id`. To add a field:

1. Add the labelled input inside the relevant `<fieldset>`, with a unique `id`.
2. Read it in the `read()` function — `<id>: $('<id>').value.trim()`.
3. Render it in `render()` inside the matching section block, following the `kv()` / `textSec()` pattern already there.
4. If it should appear in exports, add the same line to the Markdown builder (`mdText()`) and, if relevant, the standalone HTML.

Repeatable rows (sources, benchmarks) are generated by `makeRow()` and read by scanning the row containers; copy that pattern for any new repeatable group.

### Adding a governance framework

Section 7 is the extension point named in the roadmap. To add, for example, an ISO/IEC 42001 Annex A tag set:

- Add a checkbox group in the section 7 `<fieldset>`, marked with a data attribute (`data-iso`) as the NIST group uses `data-nist`.
- Collect the checked values in `read()`.
- Emit them as tags in the governance block of `render()`, `mdText()` and the HTML export, reusing the `.tag` styles. Give the new tag class its own fill so it is distinguishable from the NIST and EU AI Act tags.

### Rebranding

Change the tokens in `:root` and nothing else; no colour is hard-coded downstream. The EU AI Act risk-tag colours are intentionally outside the brand palette — leave them unless your organisation has a different risk-colour convention, in which case change the `.risk-*` classes together so the five levels stay distinct.

### Typography

Replace the Google Fonts `<link>` and the `font-family` declarations. The file already uses the HCXAI house pairing — Poppins for the wordmark and card title, Inter for everything else — so no change is needed for house consistency.

### Changing the sample or the default preparer

The sample content is in the **Load sample** handler; edit the field assignments there. The default preparer (`HCXAIResearch`) and today's date are set once near the top of the script and in the **Clear** handler.

---

## 7. Accessibility

| Feature | Implementation |
| --- | --- |
| Labels | Every input has an associated `<label>`; hints are adjacent text, not placeholder-only |
| Keyboard | All controls are native inputs, selects, checkboxes and buttons, reachable by <kbd>Tab</kbd> and operable without a pointer |
| Focus visibility | Teal focus ring with a soft outline on inputs and buttons |
| Colour | EU AI Act risk tags carry a text label as well as a colour, so the level does not depend on hue; governance tags are always labelled |
| Viewport | Responsive; columns stack below ~940 px and field grids collapse to a single column on narrow screens |

**Known limitation.** Preview updates are not announced to screen readers — there is no live region on the card. For a screen-reader user completing the form, the source of truth is the form itself, not the preview; the exported HTML or Markdown is fully linear and readable. If you need live announcement, add `aria-live="polite"` to the `#card` container.

---

## 8. Troubleshooting

| Symptom | Cause and fix |
| --- | --- |
| Fonts render as a default sans-serif | Google Fonts is blocked. Harmless — the fallbacks are declared. To remove the dependency, delete the `<link>` tags in `<head>` |
| Form cleared unexpectedly | The page was reloaded. State is in memory only, by design. Export before reloading or closing |
| **Print / PDF** does nothing | `window.print()` is blocked in the current sandboxed context. Open the file directly in a browser tab, or use the **HTML** export and print that |
| A section is missing from the card | It has no content. Empty fields are omitted deliberately. Fill a field in that section and it appears |
| A benchmark or source row will not go away | Use the **×** at the end of the row. Removing the last field's text does not remove the row |
| Markdown table looks broken in a viewer | A cell contained a pipe character; the export escapes these, but check the viewer supports GitHub-flavoured Markdown tables |
| Export filename is `model-card.md` | The **Model name** field is empty. Fill it and re-export; the filename derives from it |
| Edits to the file broke the page | Almost always a missing comma or an unescaped `"` in the script. Open the console for the parse error, or run `node --check` against the extracted script block |

---

*HCXAIResearch · Human Explainable AI governance · `HCXAI-prj04-001-M` v1.0*
