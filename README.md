# Base de Conhecimento IPlanRio

Wiki institucional persistente sobre a IPlanRio, mantida pelo Claude Code ao
longo do tempo. Toda a lógica de como isso funciona está em `CLAUDE.md` — este
README é só o "como usar no dia a dia".

## Estrutura

- `raw/` — fontes originais (despachos, ofícios, planilhas, atas, e-mails...).
  Nunca editar manualmente o conteúdo aqui, só adicionar/mover arquivos.
- `wiki/` — páginas markdown organizadas por categoria (órgãos, gerências,
  projetos, contratos, pessoas, conceitos, outputs). Compatível com Obsidian
  (abra esta pasta, ou a pasta acima com o vault, no Obsidian).
- `wiki/index.md` — ponto de partida para navegar a wiki.
- `wiki/log.md` — histórico de tudo que foi feito.

## Como usar

### Ingerir novas fontes
1. Coloque o(s) arquivo(s) novo(s) na subpasta certa de `raw/` (ex.:
   `raw/comunicacoes/` para uma ata de reunião, `raw/planilhas/` para uma
   planilha de circuitos).
2. Peça ao Claude Code, nesta pasta: **"faz o ingest dos arquivos novos em
   raw/"** (ou aponte o arquivo específico). Pode soltar vários arquivos de
   uma vez — o fluxo é otimizado para lote.
3. O Claude vai atualizar/criar páginas em `wiki/`, atualizar `index.md` e
   `log.md`, e te dar um resumo do que mudou pra você revisar.

### Fazer uma pergunta
Pergunte normalmente, ex.: **"qual o status do contrato com a Green4T?"** ou
**"quais órgãos tiveram problema de SLA no último trimestre?"**. O Claude
responde com base no que já está na wiki (markdown por padrão; pode pedir
slides ou gráfico se fizer sentido pra pergunta). Respostas mais elaboradas
costumam ser arquivadas de volta em `wiki/outputs/` — assim a próxima pergunta
parecida já parte de um contexto mais rico.

### Rodar um lint (checagem de saúde da wiki)
De vez em quando (ex.: mensalmente, ou quando a wiki estiver crescendo muito),
peça: **"roda um lint na wiki"**. O Claude aponta contradições entre páginas,
informação desatualizada, páginas órfãs, conceitos sem página própria, e
referências cruzadas faltando — e você decide o que fazer com cada achado.

## Git

Este projeto é um repositório git próprio (separado de qualquer outro git que
exista em pastas acima). Histórico de mudanças na wiki fica registrado nos
commits, além do `log.md`.
