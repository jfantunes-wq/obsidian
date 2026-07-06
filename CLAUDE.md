# CLAUDE.md — Wiki Institucional IPlanRio

Este arquivo é o **schema** deste projeto. Se você é uma instância do Claude Code
retomando este projeto "a frio", leia este arquivo inteiro antes de fazer qualquer
coisa. Ele define como as três camadas do sistema se relacionam e como executar as
três operações centrais: **ingest**, **query** e **lint**.

## 1. Arquitetura: raw / wiki / schema

Este não é um sistema RAG clássico (retrieve-and-forget). É uma **wiki persistente e
cumulativa**:

- **`raw/`** — fontes brutas, curadas e **imutáveis**. Documentos institucionais
  (despachos, ofícios, TRs, contratos, decretos, portarias), planilhas técnicas
  (circuitos, SLA, dados de rede), comunicações (emails, atas, transcripts),
  apresentações, artigos, datasets e imagens/assets. Uma vez colocado em `raw/`, um
  arquivo nunca é editado ou movido — ele é a fonte de verdade.
- **`wiki/`** — páginas markdown que você (o LLM) cria e mantém: páginas de
  entidade, páginas de conceito, `index.md` e `log.md`. O humano (Diretor de
  Operações da IPlanRio) lê essa camada, mas raramente edita diretamente.
- **`CLAUDE.md`** (este arquivo) — convenções, templates e workflows.

A wiki **não é reconstruída do zero a cada pergunta**. Cada sessão de ingest lê o
que já existe, atualiza incrementalmente, e sinaliza contradições em vez de apagar
histórico silenciosamente.

## 2. Convenções de nomenclatura

### Arquivos em `raw/`
Formato: `AAAA-MM-DD_descricao-curta-em-kebab-case.ext`
Exemplos:
- `raw/documentos/2026-03-12_despacho-certificado-serpro.pdf`
- `raw/planilhas/2026-04-01_base-consolidada-circuitos-smas.xlsx`
- `raw/comunicacoes/2026-05-20_ata-reuniao-gte-mvp.md`

Se a data real do documento não for conhecida, use a data de ingest e registre a
data real (se houver) no frontmatter da página wiki correspondente.

### Páginas em `wiki/`
Formato: `slug-kebab-case.md`, sempre dentro da subpasta da categoria certa.
Exemplos: `wiki/gerencias/gte.md`, `wiki/contratos/green4t-022-2022.md`,
`wiki/pessoas/leonardo-cavalieri.md`, `wiki/conceitos/ata-de-registro-de-precos.md`.

Slugify: minúsculas, sem acento, espaços e "/" viram `-`. Acrônimos institucionais
(GTE, GSA, GSC, GIT, SMF, DAF, SLA) podem ficar em maiúsculas no **título** da
página (H1) mesmo que o slug do arquivo esteja em minúsculas.

## 3. Frontmatter YAML — schema e exemplo

Toda página em `wiki/` (exceto `index.md` e `log.md`) deve ter frontmatter YAML no
topo:

```yaml
---
tags: [gerencia, telecom]
created: 2026-03-12
updated: 2026-05-20
related_org: IPlanRio
source_count: 4
aliases: [GTE, Gerência de Telecomunicações]
---
```

Campos:
- `tags` (obrigatório) — lista de categorias/temas (ex.: `orgao`, `gerencia`,
  `projeto`, `contrato`, `pessoa`, `conceito`, mais tags livres de assunto).
- `created` (obrigatório) — data ISO da primeira criação da página.
- `updated` (obrigatório) — data ISO da última atualização.
- `related_org` (quando relevante) — órgão/empresa relacionado.
- `source_count` (quando relevante) — quantas fontes em `raw/` alimentaram a página.
- `aliases` (opcional) — nomes alternativos, siglas, para facilitar busca no
  Obsidian/Dataview.

Use `[[wikilink]]` para qualquer referência a outra página da wiki, para que o
graph view do Obsidian funcione automaticamente.

## 4. Templates de página por categoria

### Órgão (`wiki/orgaos/`)
```markdown
---
tags: [orgao]
created: YYYY-MM-DD
updated: YYYY-MM-DD
related_org: <nome>
source_count: N
---
# <Nome do Órgão>

## Visão geral
Breve descrição do órgão e sua relação com a IPlanRio.

## Interações e histórico
Cronologia de interações relevantes, com link para `wiki/projetos/` e
`wiki/contratos/` quando aplicável.

## Pessoas-chave
- [[pessoa-x]] — cargo/papel

## Fontes
- `raw/.../arquivo.ext` — descrição curta
```

### Gerência (`wiki/gerencias/`)
```markdown
---
tags: [gerencia]
created: YYYY-MM-DD
updated: YYYY-MM-DD
aliases: [SIGLA]
---
# <Nome da Gerência> (SIGLA)

## Escopo
O que a gerência cobre.

## Liderança
[[pessoa]] — Gerente

## Metas e OKRs
Metas setoriais vigentes, com link para [[projeto]] relevantes.

## Fontes
- `raw/...` 
```

### Projeto (`wiki/projetos/`)
```markdown
---
tags: [projeto]
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: em-andamento | concluido | pausado
---
# <Nome do Projeto>

## Objetivo
## Status atual
## Marcos (milestones)
## Decisões-chave
## Envolvidos
- [[pessoa]], [[gerencia]]

## Fontes
```

### Contrato (`wiki/contratos/`)
```markdown
---
tags: [contrato]
created: YYYY-MM-DD
updated: YYYY-MM-DD
fornecedor: <nome>
numero_contrato: <numero/ano>
---
# <Fornecedor> — Contrato nº <numero>

## Objeto
## Vigência
## Status / renovações
## Órgãos envolvidos
- [[orgao]]

## Fontes
```

### Pessoa (`wiki/pessoas/`)
```markdown
---
tags: [pessoa]
created: YYYY-MM-DD
updated: YYYY-MM-DD
organizacao: <IPlanRio | orgao externo>
cargo: <cargo>
---
# <Nome>

## Papel
## Histórico de interações
## Relacionado
- [[gerencia]], [[projeto]], [[orgao]]
```

### Conceito (`wiki/conceitos/`)
```markdown
---
tags: [conceito]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
# <Nome do Conceito>

## Definição
## Uso no contexto da IPlanRio
## Onde aparece
- [[pagina]] (data)
```

## 5. `index.md` — formato de entrada

`index.md` é o ponto de navegação principal. Organizado por categoria, cada entrada
segue:

```markdown
- [[slug-da-pagina]] — descrição de uma linha (atualizado: AAAA-MM-DD)
```

Agrupado sob os cabeçalhos: `## Órgãos`, `## Diretorias`, `## Gerências`,
`## Empresas Públicas`, `## Projetos`, `## Contratos`, `## Pessoas`, `## Conceitos`,
`## Outputs`. Toda página nova ou atualizada precisa ter sua entrada em `index.md`
adicionada ou tocada (data atualizada) no mesmo ingest.

## 6. `log.md` — formato de entrada

Prefixo fixo e greppável:

```markdown
## [AAAA-MM-DD] ingest | <descrição curta da(s) fonte(s)>
- Criadas: `wiki/.../pagina.md`, ...
- Atualizadas: `wiki/.../pagina.md`, ...
- Contradições/observações: ...
```

Para queries cujo resultado foi arquivado na wiki:

```markdown
## [AAAA-MM-DD] query | <pergunta resumida>
- Output: `wiki/outputs/....md`
```

Uso pretendido para consulta rápida do histórico:
```
grep "^## \[" wiki/log.md | tail -5
```

## 7. Workflow — Ingest (batch-first)

1. Receber um ou mais arquivos novos (o dono normalmente solta vários de uma vez).
2. Para cada fonte: identificar tipo (documento, planilha, comunicação, etc.),
   copiar/salvar em `raw/<subpasta>/` com nome no padrão da seção 2 — **nunca**
   editar o conteúdo original.
3. Extrair informação relevante: entidades (órgãos, pessoas, gerências),
   projetos, contratos, conceitos, datas, decisões.
4. Para cada entidade relevante: atualizar a página existente em `wiki/` (mesclando
   informação nova, marcando o que ficou superado, nunca apagando histórico sem
   necessidade) ou criar uma página nova a partir do template da seção 4.
5. Atualizar `index.md` (entradas novas ou tocadas).
6. Acrescentar entrada em `log.md` no formato da seção 6.
7. Ao final do batch, produzir um resumo em texto (não em arquivo) do que foi
   criado/atualizado, para revisão do dono.
8. Se uma fonte contradiz algo já registrado, **não sobrescrever silenciosamente**:
   registrar a contradição na página afetada (seção "Observações" ou similar) e no
   `log.md`.

## 8. Workflow — Query

1. Ler `index.md` para localizar páginas potencialmente relevantes.
2. Abrir e ler as páginas identificadas (drill-down).
3. Sintetizar a resposta citando as páginas wiki específicas usadas (ex.: "conforme
   [[gte]] e [[meta-gte-2026]]").
4. Escolher o formato de saída conforme a seção 9.
5. Se a resposta tiver valor de reuso (comparação, análise, nova conexão), oferecer
   ao dono arquivá-la em `wiki/outputs/` como uma nova página, com entrada
   correspondente em `index.md` e `log.md` (tipo `query`).

## 9. Regra de formato de saída

- **Padrão: markdown** (página ou tabela) — usar sempre que a pergunta não pedir
  explicitamente outro formato.
- **Marp (slides)** — quando a pergunta pedir claramente uma apresentação
  (ex.: "monta um resumo em slides sobre..."). Gerar `.md` com frontmatter Marp.
- **Gráfico (matplotlib)** — quando a pergunta for quantitativa/tendência (ex.:
  "como evoluiu o número de circuitos por órgão", "tendência de SLA"). Gerar a
  imagem e referenciá-la a partir de uma página em `wiki/outputs/`.

## 10. Busca — quando reconsiderar

Hoje a navegação depende só de `index.md`. Isso é suficiente na escala atual.
**Reconsiderar** introduzir uma ferramenta de busca dedicada (ex.: `qmd` via CLI ou
como servidor MCP) quando:
- a wiki ultrapassar aproximadamente 150–200 páginas, ou
- a busca por `index.md` começar a parecer insuficiente (muito tempo para achar a
  página certa, muitos hits irrelevantes).

Quando esse ponto for atingido, propor a mudança ao dono em vez de simplesmente
implementá-la.

## 11. Não fazer

- **Nunca** editar ou apagar arquivos em `raw/` — são a fonte de verdade imutável.
- **Nunca** apagar páginas da wiki durante um ingest normal. Remoção só acontece em
  uma limpeza explícita conduzida por um lint, e somente depois que o conteúdo
  relevante foi preservado/mesclado em outro lugar.
- **Nunca** traduzir termos técnicos/institucionais (SLA, glosa, órgão, Ata de
  Registro de Preços, etc.) — preservar o termo original mesmo com a página em
  PT-BR.

## 12. Workflow — Lint

Rodar periodicamente (ou quando solicitado):
1. **Contradições** — comparar páginas que tratam do mesmo tema/entidade,
   procurando afirmações incompatíveis.
2. **Obsolescência** — claims superados por fontes mais recentes em `raw/` que
   ainda não foram refletidos na página.
3. **Páginas órfãs** — páginas em `wiki/` sem nenhum link de entrada (`[[...]]`)
   vindo de outra página ou do `index.md`.
4. **Conceitos sem página** — termos citados repetidamente em várias páginas que
   ainda não têm página própria em `wiki/conceitos/`.
5. **Referências cruzadas faltando** — menções a entidades que já têm página mas
   não estão linkadas como `[[wikilink]]`.

Reportar os achados em texto ao dono, com sugestão de ação para cada item; não
aplicar correções automaticamente sem confirmação, exceto atualizações triviais de
frontmatter (`updated:`).
