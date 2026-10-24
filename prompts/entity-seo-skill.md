# Entity SEO Skill — Any Website, 2027 Standards

- Saved: 2026-10-24
- Tags: entity-seo, schema, structured-data, ai-search, geo, topical-authority
- Status: untested variant
- Agent or model: Muse (Meta), composed in conversation on 2026-10-24

## What this does
Gives an agent a complete, portable method for building or auditing the entity SEO of any website or business: one canonical home per entity, a clear machine-readable description, a schema graph that mirrors the page, consistent facts across the web, topic clusters, and monitoring that covers both classic search and AI-generated answers. It contains no facts about any specific business; every business-specific value is an input supplied per run.

## When to use it
When building a new website, rebuilding an existing one, or auditing why a business is poorly understood, misdescribed, or not named by search engines and AI assistants. Works for a business, a person, or a product as the primary entity.

## Required context and tools
- Web access to research the business and to re-verify current search platform state (Step 0 of the prompt).
- The business's fact sheet if one exists; if not, the prompt builds it as its first step.
- Edit access to the target website (or produce the implementation as files/instructions if only auditing).

## Inputs to replace
- `[ENTITY NAME]` — the business, person, or product the run is about.
- `[ENTITY TYPE]` — Organization, LocalBusiness subtype, Person, or Product.
- `[DOMAIN]` — the site's primary domain.
- `[FACT SHEET]` — the existing fact sheet, or "none — build it" to have the run research and create it.
- `[PLATFORM]` — WordPress, plain PHP/HTML, Shopify, or other; selects the implementation branch.

## Prompt
~~~~text
You are implementing entity SEO for [ENTITY NAME] ([ENTITY TYPE]) at [DOMAIN]. Fact sheet: [FACT SHEET]. Platform: [PLATFORM].

Ground rules:
- This method is portable. Never import facts from another business. Every fact you publish comes from this entity's fact sheet or from research you do in this run.
- One entity gets one home. Never split an entity across half-pages.
- Schema must mirror what the page visibly says. Never mark up facts the page does not state.
- Consistency beats volume. Manufactured mentions, fake reviews, and mass-generated filler pages are prohibited; search engines filter them and AI systems discount them.

Step 0 — Re-verify platform state before trusting any dated fact.
Check the Google Search Central documentation changelog and current structured data guidance for changes since this snapshot (taken 2026-10-24), and apply what you find over this list:
- FAQ rich results no longer appear in Google Search as of 2026-05-07; the FAQ documentation was removed in June 2026. FAQPage markup stays valid and harmless, and question-and-answer content still earns citations, but never sell FAQ markup as a search-display tactic.
- Seven structured data types were retired on 2025-06-12: Book Actions, Course Info, Claim Review, Estimated Salary, Learning Video, Special Announcement, Vehicle Listing. Do not build for retired displays. Retirements affect display only, not rankings, and leftover markup is not penalized.
- Google states there is no special markup required for AI Overviews or AI Mode, and that llms.txt neither helps nor hurts Google visibility. Treat llms.txt as optional, never as a tactic.
- Types that carry weight: Organization (and LocalBusiness subtypes), Person, Product with offers and reviews, Article, BreadcrumbList, WebSite, WebPage.

Step 1 — Intake and fact sheet.
If no fact sheet exists, research everything public about the entity first: legal and trading names, one-sentence description, logo, founders or owners, founding date, locations and service areas, offerings, hours, contact points, and every official profile. Write it as a one-page fact sheet. Every later step reads from it, and every profile you touch gets aligned to it. Gaps you cannot verify become questions, not guesses.

Step 2 — Entity home and clear description.
Choose one stable, plain URL as the official home of the entity. In the first 100 to 150 words, state who or what it is, what it does, and who it is for, in language a smart 12-year-old would understand. Put the one-sentence definition in the first 40 to 60 words so AI systems can lift it as a passage. Dates, locations, versions, and specs count as facts; include the ones that are true.

Step 3 — Schema graph that mirrors the page.
Emit one JSON-LD @graph per page tying the nodes together with stable @id values: the entity (correct type and subtype), WebSite, WebPage, and Article or Product where relevant. Set mainEntityOfPage on the entity, about and mentions on content pages, and sameAs links to the authoritative profiles the entity controls, including a Wikidata entry where one exists. Person entities get author pages as their homes, with knowsAbout and credentials where true. Product entities keep price, availability, and review facts in sync with the visible page and any product feed.

Step 4 — Standardize facts everywhere.
Make name, description, logo, founders, dates, and key attributes identical across every profile and directory the entity manages: search business profiles, maps listings, social profiles, and industry directories. Inconsistency makes search engines guess; guessing costs the entity.

Step 5 — Map topics and supporting entities.
For each pillar topic, list 5 to 10 closely related entities a solid page on that topic would mention. Pick one term per concept and use it consistently.

Step 6 — Build pillars and clusters.
One strong pillar page per main topic, supporting pages for subtopics, each page primarily about one thing.

Step 7 — Link internally with purpose.
Link subtopic pages up to their pillar and cross-link siblings where it helps the reader. Use natural anchor text that names the thing. Never use generic anchors.

Step 8 — Answer real questions.
Cover the who, what, when, where, why, and how questions people actually ask about the entity and its topics. Answer each in one tight, self-contained passage a model can quote on its own, then expand below it if needed.

Step 9 — Label helpful media.
Use clear images, charts, or tables. Give files descriptive names, write descriptive alt text and captions.

Step 10 — Publish, then reconcile.
After publishing, update the entity's external profiles so they match the entity home. Prioritize the profiles and directories that rank for the entity's name and products.

Step 11 — Monitor and adjust.
Check what appears for the entity's name and key products in classic results and knowledge panels. Once a month, ask the major AI assistants the questions buyers ask in this market and record who gets named and cited. Track branded search volume as the north star. Review quarterly, fix stale facts promptly, and update the title year and dateModified whenever content materially changes.

Step 12 — Rinse, then go deeper.
Expand to the next set of supporting entities and questions. Depth beats breadth until each pillar feels complete.

Implementation branch (from [PLATFORM]):
- WordPress: use the SEO plugin's schema controls (for example Rank Math) for the graph basics and add a hand-written JSON-LD block for anything the plugin cannot express. Keep one source per fact.
- Plain PHP or static HTML: hand-roll the JSON-LD in the page template, driven by the same single fact source as the visible content.
- Shopify: use the theme's built-in Product and Organization output, verify it, and patch gaps in the template rather than adding a second competing graph.
- Any platform: validate the result with a structured data testing tool and confirm the rendered markup matches the visible page.

Deliverables for this run:
1. The completed worksheet: primary entity, one-sentence definition, who it is for, top 5 supporting entities, 3 user questions answered, internal links added, schema types and key properties, external profiles aligned.
2. The fact sheet (created or updated).
3. A change list separating what was implemented from what is recommended next.
~~~~

## Results observed
In the originating conversation on 2026-10-24, this method was designed from a published 12-step entity SEO playbook (source in Publication notes) and its time-sensitive claims were verified against current sources the same day: the end of FAQ rich results (2026-05-07), the June 2025 retirement of seven structured data types, and Google's stated position that no special markup is required for AI search features and that llms.txt is neutral. The portability design (intake inputs, platform branches, no baked-in business facts, mandatory re-verification step) was specified and reviewed in that conversation. The prompt has not yet been run end-to-end against a live website, and no ranking, citation, or traffic results exist yet.

## Expected output
A completed per-business worksheet, a fact sheet, implemented or implementation-ready schema and content changes for the target site, and a monitoring baseline covering classic search results and AI answers.

## Limitations and reuse notes
- The dated platform snapshot in Step 0 decays. The re-verification in that step is mandatory, not optional.
- Notability limits apply: Wikipedia and Wikidata entries are not available to every business, and third-party corroboration (reviews, directories, community presence) is partly outside the site's control.
- Outcomes depend on the accuracy of the fact sheet. Unverified facts must be flagged as questions during intake, never published as settled.

## Publication notes
The prompt wording was composed on 2026-10-24 as a distillation and modernization of Casey Keith's public article "Step-by-Step: How To Implement Entity SEO" (https://caseykeith.me/step-by-step-how-to-implement-entity-seo/), combined with platform changes verified against current search documentation coverage the same day. It is a reconstruction in new wording, not a verbatim copy of the article or of any single message from the conversation. It contains no private names, credentials, paths, or client details; all business-specific values are placeholders listed under Inputs to replace.
