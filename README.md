# Wiki Institucional IPlanRio

Base de conhecimento institucional persistente sobre a IPlanRio, mantida por um
agente LLM (Claude Code) rodando neste diretório. Toda a lógica de funcionamento
está detalhada em `CLAUDE.md` — este README é só o guia rápido do dia a dia.

## Estrutura

- `raw/` — documentos, planilhas, emails/atas etc. originais. Nunca editados.
- `wiki/` — páginas markdown organizadas por categoria (órgãos, gerências,
  projetos, contratos, pessoas, conceitos), mais `index.md` (navegação) e
  `log.md` (histórico de ingests/queries).
- `CLAUDE.md` — schema completo: convenções, templates, workflows.

## Como usar no dia a dia

### Rodar um ingest (adicionar fontes novas)
1. Abra o Claude Code neste diretório.
2. Cole/aponte os arquivos novos (pode ser vários de uma vez — o sistema é
   otimizado para lote).
3. Peça algo como: *"ingere esses arquivos na wiki"*.
4. O agente vai salvar os arquivos em `raw/`, atualizar/criar páginas em `wiki/`,
   atualizar `index.md` e `log.md`, e te dar um resumo do que foi feito.

### Fazer uma pergunta
Pergunte normalmente, ex.: *"o que já sabemos sobre o contrato da Green4T?"* ou
*"como está o andamento da meta da GTE?"*. O agente vai consultar `index.md`,
abrir as páginas relevantes e responder citando as páginas usadas. Se a resposta
for útil o suficiente para reaproveitar depois, ele vai perguntar se quer
arquivá-la em `wiki/outputs/`.

Para pedidos de apresentação, ele gera slides (Marp). Para perguntas quantitativas
(ex.: evolução de circuitos por órgão), ele gera um gráfico.

### Rodar um lint (checagem de saúde da wiki)
Peça: *"roda um lint na wiki"*. O agente procura contradições entre páginas,
informação desatualizada, páginas órfãs, conceitos sem página própria e links
faltando — e te dá um relatório com sugestões (sem aplicar mudanças automáticas,
exceto ajustes triviais de data).

### Ver o histórico rápido
```
grep "^## \[" wiki/log.md | tail -5
```

## Obsidian

Abra esta pasta como vault no Obsidian. Todas as páginas têm frontmatter YAML
compatível com Dataview e usam `[[wikilinks]]`, então o graph view e as consultas
Dataview funcionam sem configuração extra.
