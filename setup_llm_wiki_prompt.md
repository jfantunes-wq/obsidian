# Prompt for Claude Code — Setup an Institutional Knowledge Base ("LLM Wiki")

You are running inside the root directory of a new project. Your job is to **set up the
entire scaffolding** for a personal/institutional knowledge base system, following the
pattern described below. This is a one-time setup task: after this session, the
resulting structure and `CLAUDE.md` will be what future sessions rely on to ingest
sources, answer questions, and maintain the wiki.

## The pattern (background for you)

Instead of treating documents as something to retrieve-and-forget (classic RAG), the
idea is to maintain a **persistent, compounding wiki**. Raw sources are dropped into a
`raw/` folder and never modified — they are the immutable source of truth. An LLM
(you, in future sessions) reads each new source and integrates it into a `wiki/` folder
of interlinked markdown pages: updating entity pages, revising summaries, flagging
contradictions with older material, and keeping cross-references consistent. The wiki
is not rebuilt from scratch on every question — it accumulates, and each session
builds on what previous sessions already organized.

There are three layers:

1. **Raw sources** (`raw/`) — curated, immutable inputs (documents, spreadsheets,
   emails, meeting notes, etc.).
2. **The wiki** (`wiki/`) — LLM-owned markdown pages: entity pages, concept pages,
   summaries, an index, and a chronological log. You create and update this layer;
   the human reads it but rarely edits it directly.
3. **The schema** (`CLAUDE.md`) — the config file you are about to write, which
   defines folder conventions, page templates, and the ingest / query / lint
   workflows for this specific project.

Three core operations happen over time:

- **Ingest** — process one or more new raw sources, extract key information, update
  or create the relevant wiki pages, update `index.md`, and append an entry to
  `log.md`.
- **Query** — answer a question by reading `index.md` first to find relevant pages,
  then drilling into them, synthesizing an answer with citations to specific wiki
  pages. Valuable answers (comparisons, analyses, new connections) should usually be
  filed back into the wiki as new or updated pages, so exploration compounds.
- **Lint** — periodically health-check the wiki: find contradictions between pages,
  stale claims superseded by newer sources, orphan pages with no inbound links,
  concepts mentioned but lacking their own page, and missing cross-references.

## Project-specific context

This wiki is for **institutional knowledge about IPlanRio** (Empresa Municipal de
Informática da Prefeitura do Rio de Janeiro), the municipal IT company of Rio de
Janeiro. The owner is the Diretor de Operações, who oversees four gerências (GSA,
GTE, GSC, GIT) and interfaces with external stakeholders such as SMF and DAF.

Key characteristics to design around:

- **Source mix**: institutional documents (despachos, ofícios, termos de referência,
  contratos), technical spreadsheets (circuit inventories, SLA data, network data),
  and meeting notes / emails / atas. Expect very heterogeneous file types (.docx,
  .xlsx, .pdf, .eml/.msg or pasted email text, .md from clipped pages, images).
- **Wiki content language**: all wiki pages (summaries, entity pages, concept pages)
  must be written in **Brazilian Portuguese (PT-BR)**, regardless of the language of
  the raw source. Preserve original technical terms/acronyms (SLA, glosa, órgão,
  Ata de Registro de Preços, etc.) rather than translating them.
- **Ingest style**: optimize primarily for **batch ingest** — the owner will often
  drop several sources at once and expects the LLM to process them with light
  supervision, producing a clear summary of what was created/updated for review
  afterward. Still support ingesting a single source when asked.
- **Output formats for queries**: support all of the following, chosen based on what
  fits the question — markdown pages/tables (default), Marp-format slide decks for
  presentation-style answers, and matplotlib-generated charts/images for
  quantitative questions (e.g. SLA trends, circuit counts by órgão). Always default
  to plain markdown unless the question clearly calls for slides or a chart.
- **Search**: no dedicated search engine yet. Rely on `index.md` as the primary
  navigation aid for now. In `CLAUDE.md`, document a clear trigger condition for
  when to reconsider this (e.g., "once the wiki exceeds roughly 150–200 pages, or
  index-based lookup starts feeling insufficient, propose introducing a proper
  search tool such as `qmd`, either as a CLI the LLM shells out to or as an MCP
  server") — but do not build it now.
- **Version control**: initialize the project as a git repository so the wiki has
  history from the start.
- **Obsidian compatibility**: the owner uses Obsidian as the frontend. All wiki
  pages should include YAML frontmatter (at minimum: `tags`, `created`, `updated`,
  and where relevant `source_count` or `related_org`) so Obsidian's Dataview plugin
  can query the wiki later. Use `[[wikilink]]` syntax for cross-references so
  Obsidian's graph view works out of the box.

## What to build in this session

1. **Folder structure**, at minimum:
   ```
   raw/
     apresentacoes/
     artigos/
     assets/
     datasets/
     decretos/
     imagens/
     decretos/
     portarias/
     sites/
     parcerias/	
     diligencias/
     documentos/       # despachos, ofícios, TRs, contratos
     planilhas/         # circuit inventories, SLA/technical spreadsheets
     comunicacoes/      # emails, atas de reunião, transcripts
     assets/             # images/attachments referenced by raw sources
   wiki/
     index.md
     log.md
     orgaos/             # pages per órgão-cliente / external stakeholder org
     diretorias/
     gerencias/          # pages per gerência (GSA, GTE, GSC, GIT) and their scope
     empresas_publicas/
     projetos/           # pages per initiative/project (e.g. meta GTE, circuit consolidation)
     contratos/          # pages per contract/vendor (e.g. Green4T, SERPRO, F5, etc.)
     pessoas/            # stakeholder pages (internal and external)
     conceitos/          # cross-cutting technical/process concepts (SLA, glosa, Ata de Registro de Preços...)
     outputs/            # answers "filed back" into the wiki (analyses, comparisons, generated slide/chart references)
   CLAUDE.md
   ```
   Adjust subfolder names/granularity if you find a cleaner structure once you think
   it through, but keep the raw/wiki separation and the entity categories above as a
   baseline — they map to how this organization actually thinks about its work.

2. **`CLAUDE.md`** — the schema file. It must cover, at minimum:
   - A short explanation of the raw/wiki/schema architecture and the ingest/query/lint
     operations, written for a future instance of yourself picking this up cold.
   - Naming conventions for files in `raw/` and `wiki/` (e.g. slugification rules).
   - The YAML frontmatter schema for wiki pages, with a concrete example.
   - Page templates (or a description of expected sections) for each wiki category:
     órgão, gerência, projeto, contrato, pessoa, conceito.
   - The exact format for `index.md` entries and `log.md` entries (propose a
     consistent log-entry prefix, e.g. `## [YYYY-MM-DD] ingest | <source description>`,
     so it stays greppable — mention `grep "^## \[" wiki/log.md | tail -5` as the
     intended usage).
   - Step-by-step instructions for the **ingest** workflow (batch-first, as described
     above), the **query** workflow (read index → drill into pages → synthesize with
     citations → offer to file the answer back into the wiki), and the **lint**
     workflow (what to check, how to report findings).
   - The output-format decision rule for queries (markdown default; Marp for
     presentation asks; matplotlib chart for quantitative/trend asks).
   - The note about when to revisit adding a search tool (see Search section above).
   - A short "do not" section: never modify files under `raw/`; never delete wiki
     pages during normal ingest (only during an explicit lint-driven cleanup, and
     only with the content preserved/merged elsewhere first).

3. **Bootstrap `index.md` and `log.md`** with correct structure but empty/placeholder
   content, ready for the first real ingest.

4. **A short `README.md`** at the project root (in Portuguese is fine here, since it's
   for the human) explaining in a few lines how to use the system day-to-day: how to
   trigger an ingest, how to ask a question, how to run a lint pass.

5. Initialize git (`git init`) and make an initial commit with the scaffolding.

## Before you start

Ask me any clarifying questions you need about folder granularity, naming
conventions, or frontmatter fields before generating files — but do not re-ask about
anything already decided above (domain, language, ingest style, output formats,
search approach, git, Obsidian compatibility). Once confirmed, create all files
directly; don't just describe them.
