# Log — Wiki Institucional IPlanRio

> Formato das entradas, ver `CLAUDE.md` seção 6.
> Consulta rápida: `grep "^## \[" wiki/log.md | tail -5`

## [2026-07-06] setup | scaffolding inicial do projeto
- Criadas: estrutura de pastas `raw/`, `wiki/`, `CLAUDE.md`, `index.md`, `log.md`, `README.md`.
- Atualizadas: —
- Contradições/observações: nenhuma fonte real ainda ingerida; wiki vazia aguardando primeiro ingest.

## [2026-07-06] ingest | Home da intranet institucional (Iplanet)
- Fontes: `raw/sites/IPLANET.md`
- Páginas criadas: [[iplanrio]], [[daf]], [[dtgg]], [[acordo-de-resultados]]
- Páginas atualizadas: nenhuma (wiki estava vazia)
- Contradições/observações: nenhuma. Fonte é a home da intranet (teaser de
  notícias), cobertura parcial. Dois itens notáveis — agente de IA no
  WhatsApp para cidadãos e "Hub de Insights" (observabilidade) — foram
  registrados apenas como notícias em [[iplanrio]]; considerar página de
  projeto dedicada se/quando a matéria completa for ingerida. Presidência
  (PRE) e NCN mencionados mas sem página própria ainda (conteúdo insuficiente
  na fonte).

## [2026-07-06] ingest | Home do site institucional público (iplanrio.prefeitura.rio)
- Fontes: `raw/sites/Prefeitura.Iplanrio.md`
- Páginas criadas: nenhuma
- Páginas atualizadas: [[iplanrio]] (source_count 1→2; links de matéria
  completa adicionados às notícias já registradas — case Google Workspace e
  agente de IA no WhatsApp — e novo item de notícia: plataforma de
  capacitação + emprego da Prefeitura do Rio)
- Contradições/observações: nenhuma contradição. Observação: domínio público
  (iplanrio.prefeitura.rio) é distinto do domínio da intranet
  (iplanet.prefeitura.rio) — anotado em [[iplanrio]] para evitar confusão
  futura. Papel exato da IplanRio na plataforma de capacitação/emprego não
  fica claro só pela home — candidato a página de projeto se a matéria
  completa for ingerida.

## [2026-07-06] ingest | "A IPLANRIO" — identidade organizacional (1989–2024)
- Fontes: `raw/sites/A IPLANRIO.md`
- Páginas criadas: nenhuma
- Páginas atualizadas: [[iplanrio]] (source_count 2→3; nova seção "Histórico
  institucional e vinculação" com tabela de vinculação administrativa e
  principais reestruturações), [[daf]] (nova seção "Origem e evolução"),
  [[dtgg]] (nova seção "Observações")
- Contradições/observações:
  - Confirmado o significado do acrônimo GIT (Gerência de Inovação
    Tecnológica), citado como exemplo no `CLAUDE.md`, mas o registro é de
    2016 — não confirmado se ainda existe com esse nome/escopo hoje. Sem
    página própria criada.
  - Possível contradição/lacuna: a fonte menciona "Coordenadoria Técnica de
    Gestão de Pessoas (CTP)", não "Diretoria Técnica de Gente e Gestão
    (DTGG)" (nome e nível hierárquico diferentes). Registrado como observação
    em [[dtgg]] sem mesclar as entidades — precisa de fonte adicional para
    confirmar se é a mesma unidade renomeada/promovida após 2024.

## [2026-07-06] ingest | Site institucional público — lote (Presidência, identidade 2025, portfólio de serviços, legislação, políticas, Workspace)
- Fontes: `raw/sites/IDENTIDADE ORGANIZACIONAL 2025.md`, `raw/sites/Presidência.md`,
  `raw/sites/Contratos e Licitações.md`, `raw/sites/Desenvolvimento de Soluções Integradas.md`,
  `raw/sites/Rede e Conectividade.md`, `raw/sites/Serviços de Atendimento e Suporte ao Cliente.md`,
  `raw/sites/Serviços de Datacenter.md`, `raw/sites/Padronização - Produtos de TI e Normatizações.md`,
  `raw/sites/Legislações específicas.md`, `raw/sites/POLÍTICAS E NORMAS.md`,
  `raw/sites/Estrutura-Organizacional-IplanRio.png (1435×1078).md`,
  `raw/sites/Workspace » Ambiente colaborativo ....md`
- Páginas criadas: [[presidencia]], [[thiago-trabach]],
  [[fernando-ivo-pimentel-cavalcante]], [[ingrid-gomes]],
  [[workspace-prefeitura-rio]]
- Páginas atualizadas: [[iplanrio]] (source_count 3→12; novas seções Missão/
  Visão/Valores, Portfólio de serviços, Legislação aplicável, Políticas e
  normas internas; estrutura organizacional agora referencia [[presidencia]])
- Contradições/observações:
  - **Vice-Presidência**: `A IPLANRIO.md` afirma extinção em 2021 (Decreto
    48.561); `Presidência.md` (site atual) lista um Vice-Presidente em
    exercício (Fernando Ivo Pimentel Cavalcante) e uma nova Vice-Presidência
    de Produtos e IA — VPIA (Ingrid Gomes). Cargo foi recriado em algum
    momento entre 2021 e a captura de 2026; ato exato não identificado.
    Registrado em [[presidencia]] sem sobrescrever a informação de 2021.
  - `Estrutura-Organizacional-IplanRio.png` é apenas um link de imagem — não
    processada (não tenho o organograma visual). Poderia resolver a dúvida
    DTGG vs. CTP e o estado atual das gerências (GIT etc.) se baixada/lida;
    fica como ação pendente, sujeita a autorização do dono antes de baixar.
  - `Contratos e Licitações.md` e `POLÍTICAS E NORMAS.md` só trouxeram
    títulos/links de categorias e documentos (PDFs), sem corpo de texto —
    registrados como referência em [[iplanrio]], sem conceito/página própria
    inventado a partir de títulos isolados.
  - Roster de ~45 órgãos participantes do rollout do Workspace foi registrado
    em [[workspace-prefeitura-rio]] como lista crua (acrônimos), sem criar
    páginas de órgão individuais — não há contexto suficiente por órgão
    ainda.

## [2026-07-06] ingest | Organograma oficial IplanRio (Decreto Rio nº 56.627/2025)
- Fontes: `raw/assets/2026-07-06_estrutura-organizacional-iplanrio.png`
  (baixada com autorização do dono a partir do link em
  `raw/sites/Estrutura-Organizacional-IplanRio.png (1435×1078).md`)
- Páginas criadas: nenhuma
- Páginas atualizadas: [[iplanrio]] (seção "Estrutura organizacional"
  reescrita com organograma completo; source_count 12→13), [[dtgg]] (posição
  na estrutura + observação CTP marcada como resolvida), [[daf]] (posição na
  estrutura), [[presidencia]] (confirma duas Vice-Presidências; contradição
  de 2021 marcada como resolvida)
- Contradições/observações:
  - **Resolvido**: Vice-Presidência confirmada ativa (na verdade, duas:
    Produtos e IA e Operações) — supera a informação de extinção em 2021.
  - **Resolvido**: DTGG confirmado como nome/nível hierárquico atual e
    correto (reporta à Presidência); a "Coordenadoria Técnica de Gestão de
    Pessoas (CTP)" de `A IPLANRIO.md` foi provavelmente promovida/renomeada
    para DTGG entre 2024 e ago/2025 — ato exato não identificado.
  - **Resolvido**: GIT (Gerência de Inovação Tecnológica) não aparece no
    organograma atual — parece ter sido descontinuada/renomeada desde 2016.
  - **Correção**: NCN é subordinado à Diretoria de Planejamento e Novos
    Negócios (via Vice-Presidência de Operações), não uma unidade de topo.
  - **Inferência não confirmada**: a Vice-Presidência de Operações
    provavelmente corresponde ao cargo de Fernando Ivo Pimentel Cavalcante
    (fonte de texto só o chama de "Vice-Presidente", sem qualificador) —
    nenhuma fonte confirma essa correspondência explicitamente. Registrado
    como inferência em [[presidencia]].
  - Muitas unidades novas no organograma (Diretoria de Experiência Digital,
    Diretoria de Dados IA, Diretoria de Sistemas, Diretoria de Operações,
    etc.) foram listadas apenas como nós da árvore em [[iplanrio]] — não
    criei páginas individuais para elas por enquanto (só temos o nome da
    caixa, sem escopo/liderança/histórico); candidatas a página própria se/
    quando houver fonte com mais conteúdo sobre cada uma.

## [2026-07-06] ingest | Artigo Karpathy — padrão LLM Wiki
- Fontes: `raw/artigos/2026-07-02_karpathy-llm-wiki-pattern.pdf`
- Páginas criadas: [[llm-wiki-pattern]]
- Páginas atualizadas: nenhuma
- Contradições/observações: nenhuma. Fonte é meta — não é conteúdo
  institucional da IPlanRio, e sim o documento/prompt-base (tweet de Karpathy
  + "idea file") que inspirou a arquitetura raw/wiki/CLAUDE.md deste próprio
  projeto. Tratado como conceito transversal em vez de forçar em categoria
  institucional (órgão/projeto/pessoa) que não se aplica. A marca "DascIA
  Academy" no rodapé do PDF é só a origem do material de treinamento — sem
  relação com a IPlanRio, não gerou página própria.

## [2026-07-06] ingest | Compras e licitações (site institucional público) — lote
- Fontes: `raw/sites/Atas de Registro de Preços.md`,
  `raw/sites/Licitações - Editais e termos de referências.md`,
  `raw/sites/Consultas Públicas.md`, `raw/sites/Consulta Pública 012025.md`,
  `raw/sites/Dispensa Eletrônica.md`,
  `raw/sites/Estudo Técnico Preliminar (ETP).md`,
  `raw/sites/Fiscalização de Contratos - regulamentação.md`,
  `raw/sites/E-COMPRAS RIO - Você ligado nas Licitações da Prefeitura do Rio.md`,
  `raw/sites/Untitled.md` a `Untitled 16.md` (17 arquivos — todos capturas
  vazias do clipper ao tentar clipar URLs de PDF; só título/URL aproveitados
  como referência onde relevante)
- Páginas criadas: [[ata-de-registro-de-precos]], [[pregao-eletronico]],
  [[consulta-publica]], [[dispensa-eletronica]], [[estudo-tecnico-preliminar]],
  [[fiscalizacao-de-contratos]], [[f5-networks]], [[red-hat]], [[trendmicro]],
  [[atlassian-jira]], [[checkpoint]]
- Páginas atualizadas: [[iplanrio]] (source_count 13→21; novos links de
  cross-reference para os conceitos de compras; nota sobre Regulamento de
  Parcerias), [[workspace-prefeitura-rio]] (possível correspondência com PE
  1061/2023, não confirmada)
- Contradições/observações:
  - Nenhuma contradição. Os 17 arquivos "Untitled" são capturas vazias do Web
    Clipper (tentou clipar binários de PDF, sem corpo de texto) — títulos/
    URLs aproveitados como referência nas páginas de conceito relevantes
    (fiscalização, ETP, licitações, contratos), mas nenhuma invenção de
    conteúdo a partir deles.
  - "Consulta Pública 01/2025" (Tomada de Subsídios para Edital de
    Contratação de Soluções de Software) tem numeração parecida mas parece
    ser um processo distinto das consultas "0001/2025" e "002/2025" —
    tratado como processo separado em [[consulta-publica]], não mesclado.
  - Criei páginas de contrato só para fornecedores com histórico recorrente
    de múltiplos pregões (F5, Red Hat, Trendmicro, Atlassian/Jira,
    Checkpoint); os demais ~20 pregões (Autodesk, Cisco, Microsoft, seguro,
    limpeza, etc.) ficaram consolidados como lista em [[pregao-eletronico]]
    em vez de uma página por fornecedor — a maioria é edital único sem
    histórico de renovação capturado ainda.
  - "Guia de Acesso aos Contratos" e "Regulamento de Licitações e Contratos"
    e "Regulamento de Parcerias" da IplanRio foram só referenciados por
    título/URL (arquivos Untitled vazios) — conteúdo real ainda não
    ingerido; candidatos a aprofundamento se o PDF completo for adicionado
    a `raw/`.

## [2026-07-06] ingest | Página "Estrutura" da intranet (organograma com líderes nomeados)
- Fontes: `raw/sites/Presidência - PRES.md` a `Presidência - PRES 47.md` (48
  arquivos, todos com corpo idêntico — mesma captura duplicada 48 vezes;
  tratados como uma única fonte)
- Páginas criadas: [[rafael-casado]], [[debora-de-barros-augusto]],
  [[gabriel-gazola-milan]] (únicos líderes com biografia própria capturada;
  os demais ~30 líderes nomeados foram incorporados apenas à árvore
  organizacional em [[iplanrio]] e às páginas [[daf]], [[dtgg]],
  [[presidencia]], sem página de pessoa individual — teriam conteúdo thin,
  só nome sem biografia)
- Páginas atualizadas: [[iplanrio]] (árvore organizacional reescrita com
  líder de cada unidade; source_count 21→22), [[presidencia]] (Vice-
  Presidência de Operações confirmada = Fernando Ivo Pimentel Cavalcante;
  líderes das unidades diretamente subordinadas), [[daf]] (líder João
  Cypriano + líderes das subunidades), [[dtgg]] (líder Iris Badaró + líder
  da GAP)
- Contradições/observações:
  - **Correção importante sobre GIT**: o ingest anterior registrou "GIT não
    aparece mais no organograma" — isso estava **errado**. GIT existe e
    aparece no organograma atual, mas seu significado mudou: era "Gerência
    de Inovação Tecnológica" em 2016 e hoje é **"Gerência de Infraestrutura
    e Tecnologia"** (líder: Luciana Santos, sob a Diretoria de Operações).
    Mesmo acrônimo, unidade/escopo diferentes — corrigido em [[iplanrio]].
  - **Resolvida a inferência pendente**: Vice-Presidência de Operações =
    cargo de Fernando Ivo Pimentel Cavalcante, agora confirmado por esta
    fonte (antes era só inferência não confirmada).
  - **Novidade**: GSA (Gerência de Suporte e Atendimento, Márcio Castro) e
    GTE (Gerência de Telecomunicações) confirmados como os acrônimos citados
    de exemplo no `CLAUDE.md`. **GSC não aparece em nenhuma fonte até
    agora** — acrônimo do schema segue não confirmado.
  - **Não resolvido**: "Assessoria Especial para Parcerias (AEP)", liderada
    por Simone Torres, aparece na intranet mas não no organograma-imagem do
    Decreto 56.627/2025 — pode ser unidade mais nova ou a imagem estar
    incompleta/desatualizada.
  - Observação lateral (não registrada na wiki, só para o dono): o líder da
    Diretoria de Operações (DOP) listado na fonte é "Jorge Antunes" — mesmo
    nome do usuário do git deste repositório. Pode ser coincidência ou o
    próprio dono do projeto; não assumido/verificado na wiki.

## [2026-07-06] ingest | Verificação de 2 novos arquivos (sem conteúdo novo)
- Fontes verificadas: `raw/sites/Diretoria de Operações - DOP.md`,
  `raw/sites/Gerência de Segurança - GDS.md`
- Páginas criadas/atualizadas: nenhuma
- Contradições/observações: nenhuma. `Diretoria de Operações - DOP.md` é
  outra duplicata da mesma página "Estrutura" da intranet já ingerida em
  [[iplanrio]]/[[presidencia]]/[[daf]]/[[dtgg]] (diff mostra 1 caractere de
  diferença — um `[` faltando na primeira linha, artefato do clipper; corpo
  substantivo idêntico). `Gerência de Segurança - GDS.md` é uma captura vazia
  do clipper (só o título, sem corpo), mesmo padrão dos arquivos "Untitled"
  anteriores. Nenhum conteúdo novo para ingerir.
