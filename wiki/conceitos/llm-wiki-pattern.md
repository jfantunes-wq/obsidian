---
tags: [conceito, meta]
created: 2026-07-06
updated: 2026-07-06
aliases: [LLM Wiki, Karpathy LLM Wiki Pattern]
---
# LLM Wiki Pattern

## Definição
Padrão para construir bases de conhecimento pessoais/institucionais usando
LLMs, popularizado por um tweet e "idea file" de Andrej Karpathy (2026).
Diferente de RAG clássico (retrieve-and-forget, onde o LLM re-descobre o
conhecimento a cada pergunta), o LLM constrói e mantém uma **wiki
persistente e cumulativa**: uma coleção estruturada e interligada de arquivos
markdown que fica entre o usuário e as fontes brutas.

Três camadas:
- **Raw sources** — coleção curada e imutável de documentos-fonte.
- **Wiki** — arquivos markdown gerados/mantidos pelo LLM (páginas de
  entidade, conceito, resumos, índice, log). O LLM escreve; o humano lê.
- **Schema** (`CLAUDE.md`/`AGENTS.md`) — documento que define convenções,
  templates e workflows de ingest/query/lint.

Operações centrais: **Ingest** (nova fonte → LLM lê, extrai, integra na wiki
existente, atualiza índice e log), **Query** (pergunta → LLM busca no
índice, sintetiza resposta citando páginas, pode arquivar o output de volta
na wiki) e **Lint** (health-check periódico: contradições, claims
desatualizados, páginas órfãs, referências cruzadas faltando).

## Uso no contexto da IPlanRio
Este projeto (`F:\IPLANRIO`) é uma implementação direta desse padrão: a
estrutura `raw/` / `wiki/` / `CLAUDE.md` deste repositório, e os workflows de
Ingest/Query/Lint definidos no schema, seguem exatamente a arquitetura
descrita aqui. `raw/artigos/2026-07-02_karpathy-llm-wiki-pattern.pdf` é o
próprio documento-fonte que inspirou o setup inicial do projeto (usado para
gerar o prompt que criou a primeira versão do `CLAUDE.md`).

## Onde aparece
- `CLAUDE.md` (schema deste projeto) — implementa o padrão descrito aqui
- [[iplanrio]] e demais páginas da wiki — são o resultado prático do padrão
  aplicado ao domínio institucional da IPlanRio

## Fontes
- `raw/artigos/2026-07-02_karpathy-llm-wiki-pattern.pdf`
