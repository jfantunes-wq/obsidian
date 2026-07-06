# IPlanRio — Base de Conhecimento Institucional (LLM Wiki)

Este projeto é uma wiki institucional persistente e cumulativa sobre a IPlanRio
(Empresa Municipal de Informática da Prefeitura do Rio de Janeiro), mantida por você
(Claude) ao longo de múltiplas sessões. Este arquivo é o schema: define convenções,
templates e os workflows de ingest/query/lint. Leia-o por completo antes de executar
qualquer uma dessas operações.

## Arquitetura: raw / wiki / schema

- **`raw/`** — fontes originais, imutáveis. Nunca editar, renomear conteúdo ou apagar
  um arquivo aqui depois de adicionado (mover para reorganizar pastas é aceitável,
  editar o conteúdo não). É a fonte da verdade.
- **`wiki/`** — páginas markdown que você cria e mantém: páginas de entidade, de
  conceito, resumos, `index.md` e `log.md`. O dono do projeto lê esta camada, mas
  raramente edita diretamente.
- **Este `CLAUDE.md`** — o schema. Convenções de nomenclatura, frontmatter, templates
  de página e os três workflows abaixo.

A wiki **não é reconstruída do zero a cada pergunta**. Ela acumula: cada sessão
constrói em cima do que sessões anteriores já organizaram. Ao fazer ingest de uma
nova fonte, primeiro verifique se já existe página relevante em `wiki/` para
atualizar antes de criar uma nova.

## Convenções de nomenclatura

### Slugs
- Minúsculas, sem acento, espaços viram hífen: `Green4T` → `green4t`,
  `Ata de Registro de Preços` → `ata-de-registro-de-precos`.
- Siglas mantêm-se em minúsculo no slug mas podem aparecer em maiúsculo no título
  da página (`# SLA` com arquivo `wiki/conceitos/sla.md`).
- Nomes de pastas seguem a mesma regra (sempre minúsculas, sem acento) — **nunca
  crie uma pasta que difira de outra existente apenas por maiúscula/minúscula**:
  o filesystem do Windows é *case-insensitive*, então `raw/` e `RAW/` são a
  **mesma pasta fisicamente**, mesmo aparecendo com grafias diferentes. Um
  `mkdir` com case diferente não cria pasta nova — ele se funde silenciosamente
  na existente, e um `rm -rf` subsequente apaga as duas "visões" de uma vez.
  Sempre confira `find <nome> -type d` antes de criar/renomear pastas se houver
  qualquer dúvida sobre uma pasta já existir com outra grafia.

### Arquivos em `raw/`
- Preserve o nome original quando ele já carrega identificadores úteis (número de
  protocolo, número de despacho, data), ex.: `raw/documentos/TCM/UNISYS/040_101957_2025 - P042.pdf`.
- Quando o nome original for genérico ou sem sentido fora de contexto (ex.:
  `IMG_2384.jpg`, `Sem título.docx`), renomeie ao ingerir para
  `YYYY-MM-DD_descricao-curta.ext` (slug na descrição).
- Organize por subpasta dentro do tipo quando fizer sentido (ex.:
  `raw/documentos/<ORGAO_OU_FORNECEDOR>/arquivo.pdf`), como já ocorre com
  `raw/documentos/TCM/UNISYS/`.

### Páginas em `wiki/`
- Um arquivo por entidade/conceito: `wiki/<categoria>/<slug>.md`.
- Nome do arquivo = slug do título da página.

## Frontmatter YAML (compatibilidade Obsidian)

Toda página em `wiki/` deve começar com frontmatter YAML. Campos mínimos:
`tags`, `created`, `updated`. Adicione `source_count` (nº de fontes em `raw/`
que alimentaram a página) e/ou `related_org` quando fizer sentido.

```yaml
---
tags: [contrato, fornecedor, gte]
created: 2026-07-02
updated: 2026-07-02
source_count: 3
related_org: TCM
---
```

Use `[[wikilink]]` (sem extensão `.md`) para toda referência cruzada, para o
grafo do Obsidian funcionar sem configuração extra.

## Templates de página por categoria

Cada template abaixo é a lista mínima de seções esperadas. Adapte conforme a
fonte disponível, mas não invente seções vazias.

### Órgão (`wiki/orgaos/<slug>.md`)
```markdown
---
tags: [orgao]
created: YYYY-MM-DD
updated: YYYY-MM-DD
related_org: <sigla>
---
# <Nome do Órgão>

## Sobre
Breve descrição do órgão e sua relação com a IPlanRio.

## Contatos-chave
- [[pessoa-slug]] — cargo

## Interações relevantes
Cronologia curta de despachos, ofícios, reuniões relevantes (com links para
`raw/` e para [[conceitos]] ou [[contratos]] relacionados).

## Contratos/Projetos relacionados
- [[contrato-slug]]
- [[projeto-slug]]
```

### Gerência (`wiki/gerencias/<slug>.md`)
```markdown
---
tags: [gerencia]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
# <GSA|GTE|GSC|GIT>

## Escopo
O que a gerência cobre.

## Responsável
[[pessoa-slug]]

## Projetos ativos
- [[projeto-slug]]

## Contratos sob gestão
- [[contrato-slug]]
```

### Projeto (`wiki/projetos/<slug>.md`)
```markdown
---
tags: [projeto]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
# <Nome do Projeto/Iniciativa>

## Objetivo
## Status atual
## Gerência responsável
[[gerencia-slug]]

## Marcos / cronologia
## Fontes
- `raw/.../arquivo.ext`
```

### Contrato (`wiki/contratos/<slug>.md`)
```markdown
---
tags: [contrato, fornecedor]
created: YYYY-MM-DD
updated: YYYY-MM-DD
related_org: <fornecedor>
---
# <Fornecedor> — <objeto do contrato>

## Objeto
## Vigência
## Valor / condições
## SLA e penalidades (glosa)
## Histórico / aditivos
## Órgãos e projetos relacionados
- [[orgao-slug]]
- [[projeto-slug]]
```

### Pessoa (`wiki/pessoas/<slug>.md`)
```markdown
---
tags: [pessoa]
created: YYYY-MM-DD
updated: YYYY-MM-DD
related_org: <orgao ou gerencia>
---
# <Nome>

## Papel / cargo
## Organização
[[orgao-slug]] ou [[gerencia-slug]]

## Envolvimento em projetos/contratos
- [[projeto-slug]]
```

### Conceito (`wiki/conceitos/<slug>.md`)
```markdown
---
tags: [conceito]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
# <Termo> (ex.: SLA, Glosa, Ata de Registro de Preços)

## Definição
## Como se aplica no contexto da IPlanRio
## Onde aparece
- [[contrato-slug]]
- [[orgao-slug]]
```

## `index.md` — formato

`index.md` é o ponto de entrada de navegação (não há motor de busca ainda — ver
seção "Busca" abaixo). Estrutura:

```markdown
# Índice — Base de Conhecimento IPlanRio

## Órgãos
- [[orgao-slug]] — uma linha de contexto

## Gerências
- [[gerencia-slug]] — uma linha de contexto

## Projetos
## Contratos
## Pessoas
## Conceitos
## Outputs recentes
```

Ao ingerir, adicione/atualize a linha correspondente. Ao criar uma página nova,
ela é obrigatória no índice — página sem entrada no índice é órfã.

## `log.md` — formato

Cada operação (ingest, query relevante filed back, lint) gera uma entrada.
Prefixo fixo para permanecer *greppable*:

```markdown
## [YYYY-MM-DD] ingest | <descrição curta da(s) fonte(s)>
- Fontes: `raw/.../arquivo1.ext`, `raw/.../arquivo2.ext`
- Páginas criadas: [[slug-a]], [[slug-b]]
- Páginas atualizadas: [[slug-c]]
- Contradições/observações: <ou "nenhuma">
```

```markdown
## [YYYY-MM-DD] query | <pergunta resumida>
- Páginas consultadas: [[slug-a]], [[slug-b]]
- Output arquivado em: `wiki/outputs/<slug>.md` (ou "não arquivado")
```

```markdown
## [YYYY-MM-DD] lint | <escopo do lint>
- Achados: <resumo curto>
```

Uso pretendido para consulta rápida ao histórico:
```
grep "^## \[" wiki/log.md | tail -5
```

## Workflow: Ingest

Otimizado para **lote** — o dono normalmente solta várias fontes de uma vez.

1. Liste os arquivos novos em `raw/` (o dono indica quais, ou compare com a
   última entrada de `log.md`).
2. Para cada fonte, leia o conteúdo (extraia texto de PDF/DOCX/XLSX conforme
   necessário).
3. Identifique entidades mencionadas (órgãos, pessoas, contratos, projetos,
   conceitos) e verifique em `index.md` se página já existe.
4. Atualize páginas existentes (adicione seção de cronologia/histórico, não
   sobrescreva conteúdo anterior sem necessidade) ou crie novas usando o
   template da categoria.
5. Ao atualizar uma página, se a nova fonte contradiz algo já escrito, **não
   apague a informação antiga silenciosamente** — registre a contradição
   explicitamente na página (ex.: "~~valor anterior~~ → novo valor, conforme
   `raw/.../fonte.pdf` de DD/MM/AAAA") e mencione em `log.md`.
6. Atualize `index.md` com as entradas novas/alteradas.
7. Adicione entrada em `log.md` no formato acima.
8. Ao final do lote, produza um resumo claro para o dono revisar: o que foi
   criado, o que foi atualizado, e quaisquer contradições/ambiguidades que
   precisam de confirmação humana.

## Workflow: Query

1. Leia `index.md` primeiro para localizar páginas relevantes.
2. Abra as páginas identificadas (e suas páginas linkadas via `[[...]]`,
   quando relevante) para reunir contexto.
3. Sintetize a resposta citando páginas específicas da wiki (e, quando útil,
   o arquivo de `raw/` original).
4. Escolha o formato de output (ver regra abaixo).
5. Ofereça arquivar a resposta de volta na wiki — respostas valiosas (análises,
   comparações, conexões novas) normalmente devem virar página em
   `wiki/outputs/`, linkada a partir de `index.md`, com entrada em `log.md`.

### Regra de formato de output
- **Markdown** (páginas/tabelas) — default, use a menos que a pergunta peça
  claramente outra coisa.
- **Slides Marp** — quando o pedido for explicitamente para apresentação.
- **Gráfico matplotlib** — quando a pergunta for quantitativa/de tendência
  (ex.: evolução de SLA, número de circuitos por órgão ao longo do tempo).

## Workflow: Lint

Health-check periódico da wiki. Ao rodar, verifique:

- **Contradições** entre páginas (mesmo fato descrito de forma diferente em
  duas páginas sem uma apontar para a outra).
- **Claims desatualizados** — informação superada por fonte mais recente mas
  ainda escrita como atual.
- **Páginas órfãs** — sem nenhum link de entrada (`[[slug]]` apontando para
  elas) e sem entrada em `index.md`.
- **Conceitos mencionados mas sem página própria** — termos técnicos citados
  repetidamente (SLA, glosa, etc.) que ainda não têm `wiki/conceitos/<slug>.md`.
- **Referências cruzadas faltantes** — página A menciona entidade que já tem
  página B, mas sem usar `[[B]]`.

Relate os achados como lista objetiva (arquivo + problema + sugestão). Não
corrija automaticamente sem listar primeiro — decisões de merge/remoção de
página são do dono (ver seção "Não fazer").

## Busca

Não há motor de busca dedicado — `index.md` é o mecanismo de navegação
principal por enquanto. **Gatilho para reconsiderar**: quando a wiki
ultrapassar aproximadamente 150–200 páginas, ou quando a busca via índice
começar a parecer insuficiente (dono precisa perguntar "onde está X" com
frequência sem achar rápido), proponha introduzir uma ferramenta de busca
dedicada (ex.: `qmd`), seja como CLI que você chama via shell, seja como
servidor MCP. Não construir isso agora.

## Não fazer

- Nunca modifique o conteúdo de arquivos dentro de `raw/` — eles são a fonte
  da verdade imutável. Mover para reorganizar pastas é aceitável.
- Nunca apague páginas de `wiki/` durante um ingest normal. Remoção só ocorre
  como resultado explícito de um lint, com o conteúdo já preservado ou
  mesclado em outra página antes da remoção.
- Nunca crie uma pasta cuja grafia difira de outra existente apenas por
  maiúscula/minúscula (ver seção de nomenclatura) — no Windows isso é a mesma
  pasta fisicamente e pode causar perda de dados em operações de limpeza
  subsequentes.
