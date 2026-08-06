# InovaMA · PVCIST

**Plataforma de Valoração Comunitária e Inovação Social Territorial (PVCIST)** — um protótipo de infraestrutura inteligente para gerar, organizar, valorizar e transformar o conhecimento sobre — e produzido por — comunidades rurais, povos e comunidades tradicionais, agricultores familiares, instituições de pesquisa e gestores públicos do Maranhão. Desenvolvido a partir da proposta conceitual da Embrapa Maranhão.

🔗 **Acesse:** [https://aluisiopereirae.github.io/InovaMA/](https://aluisiopereirae.github.io/InovaMA/)

Todo o site é um único arquivo estático (`index.html`, HTML + CSS + JavaScript, sem build/servidor), incluindo o **Módulo 4 — Mapa dinâmico de valoração comunitária territorial**, construído com [Leaflet](https://leafletjs.com/).

---

## O que há no mapa

O mapa trabalha em **duas escalas territoriais** ao mesmo tempo:

1. **21 microrregiões geográficas do Maranhão** — a unidade territorial usada pelo *Atlas da Bioeconomia Inclusiva na Amazônia — Encarte Maranhão* (Embrapa, 2025), com limites reais (malha municipal do IBGE dissolvida por microrregião). Cada microrregião tem um dossiê completo: indicadores brutos, as quatro valorações (objetiva, percebida, social, potencial), o índice-síntese IVC e a priorização (matriz IAC × INV) para inovação social.

2. **141 comunidades e territórios menores**, dentro das 21 microrregiões — a camada "Comunidades e territórios" no mapa, que pode ser ligada/desligada e filtrada por tipo:

   | Tipo | Quantidade | Geometria | Fonte |
   |---|---|---|---|
   | 🟫 Território quilombola | 80 | Polígono oficial real | IBGE — Censo Demográfico 2022, Territórios Quilombolas oficialmente delimitados (2ª apuração) |
   | 🟦 Terra Indígena | 20 | Polígono oficial real | FUNAI (geoserver.funai.gov.br) |
   | 🟩 Unidade de Conservação / RESEX federal | 15 | Polígono oficial real | ICMBio / INDE (Infraestrutura Nacional de Dados Espaciais) |
   | 🟨 Distrito ou povoado rural | 26 | Ponto aproximado (raio de 3 km) | IBGE — Divisão Territorial Brasileira; coordenadas aproximadas via OpenStreetMap/Nominatim |

   Cada comunidade é desenhada com o **polígono oficial real** sempre que ele existe (territórios já delimitados/demarcados/criados por decreto). Quando não há demarcação formal conhecida — caso dos distritos e povoados —, o local aparece como um **ponto com um círculo aproximado**, nunca como um contorno inventado. O popup de cada item mostra nome, tipo, município(s), situação/fase, área e a fonte exata com o ano.

   Um seletor de **ano** permite acompanhar a evolução histórica de três indicadores com série temporal real: população residente (Censo 2010 → 2022), PIB per capita (IBGE, 2010–2023, anual) e % de população rural (2010 → 2022).

### Por que não "todas" as comunidades rurais do Maranhão?

Não existe, em nenhuma fonte pública — nem no IBGE, no INCRA, na FUNAI ou no ICMBio —, um cadastro único, geolocalizado e verificável de *todos* os povoados e aglomerados rurais do estado (são milhares de lugarejos informais, sem registro fundiário). O que existe, e é o que este mapa usa, são os conjuntos **oficialmente reconhecidos e demarcados**: territórios quilombolas certificados/delimitados, terras indígenas, unidades de conservação/reservas extrativistas e distritos oficiais do IBGE. Isso é o mais completo e ao mesmo tempo o mais preciso que é possível afirmar com fontes reais — cobrir "todas" as comunidades exigiria inventar coordenadas para lugares sem registro público, o que este projeto deliberadamente evita.

---

## Atualização de dados — 06/08/2026

Esta rodada corrigiu um problema estrutural do dataset anterior: **20 das 21 microrregiões estavam marcadas no próprio código como `real:false`** (dados ilustrativos/placeholder, com o aviso explícito "substitua pelos dados reais antes de usar em decisões"). Os indicadores abaixo foram recalculados com fontes oficiais atuais para as **21 microrregiões**:

| Indicador | Fonte | Ano |
|---|---|---|
| População residente, área, densidade | IBGE — Censo Demográfico 2022 | 2022 (+série 2010) |
| % de população rural | IBGE — Censo Demográfico 2022 | 2022 (+série 2010) |
| PIB per capita | IBGE — Produto Interno Bruto dos Municípios | 2023 (+série anual 2010–2023) |
| % de estabelecimentos de agricultura familiar | IBGE — Censo Agropecuário | 2017 |
| Gini fundiário (concentração de área agropecuária) | IBGE — Censo Agropecuário (cálculo próprio a partir da distribuição de área por estabelecimento) | 2017 |
| Nº de produtos de extração vegetal com produção | IBGE — Censo Agropecuário | 2017 |
| Nº de categorias territoriais coletivas / % de área em territórios coletivos | Cálculo geoespacial próprio, cruzando os territórios quilombolas (INCRA/IBGE), terras indígenas (FUNAI) e UCs/RESEX (ICMBio) com o polígono de cada microrregião | 2022–2025 |

Os **índices compostos** — as quatro valorações, o IVC, o IAC (aptidão), o INV (necessidade) e o quadrante de priorização — foram **recalculados** com a mesma fórmula de normalização min-max descrita na aba "Metodologia" do site, agora aplicada sobre os indicadores atualizados.

### O que ainda não foi recalculado (e por quê)

Os campos abaixo continuam com a **estimativa original do Atlas da Bioeconomia Inclusiva (Embrapa, 2025)**, porque não têm uma fonte pública de download direto e estruturado no nível de microrregião que pudesse ser verificada com o mesmo rigor nesta rodada:

- **Cobertura florestal nativa / desmatamento acumulado** — MapBiomas / INPE-PRODES publicam séries anuais reais (1985–2024), mas apenas por município em planilhas volumosas; falta reagregar para as 21 microrregiões.
- **IVS (Índice de Vulnerabilidade Social) e IVS · capital humano** — IPEA, Atlas da Vulnerabilidade Social, base 2010. O IPEA lançou em 2024–2025 uma atualização metodológica usando a PNAD Contínua compatibilizada com o Censo 2022, mas por ora disponível em nível nacional/UF, não por microrregião.
- **IDHM** — Atlas Brasil / PNUD. **Esta é, de fato, a edição mais recente existente**: o IDHM municipal não foi recalculado desde o Censo 2010 — não há "IDHM 2022" oficial publicado. Não fabricamos um valor mais novo; mantemos 2010 rotulado com essa ressalva explícita na interface.
- **% de famílias em pobreza** — estimativa original do Atlas (2010).
- **IPS-Brasil geral e seus três componentes** (necessidades básicas, conhecimento básico, informação/comunicação) — Imazon publica hoje a edição **IPS Brasil 2026** por município (a mais recente), mas a reagregação para as 21 microrregiões e a validação linha a linha ficaram fora do prazo desta rodada.

O dossiê de **cada** território no mapa mostra, indicador a indicador, um selo **✓** (fonte oficial atual, ago/2026) ou **⏳** (estimativa do Atlas 2025, ainda não recalculada) — para que nenhum número pareça mais confiável do que realmente é.

### Como contribuir com a próxima atualização

1. Baixe a série municipal do indicador (MapBiomas, IPEA, Imazon, IBGE) para o Maranhão.
2. Agregue por microrregião — para variáveis de contagem/soma (população, área, PIB, nº de produtos), some os 217 municípios por `microrregiao.id`; para percentuais, calcule a razão das somas (não a média das médias).
3. Atualize o campo correspondente em `DADOS_MAPA.dados[<micro_id>].ind` dentro de `index.html` e mova o nome do campo de `camposEstimativaAtlas2025` para `camposReais` em `qualidade`.
4. Rode a normalização min-max (mesma fórmula da aba Metodologia) para recalcular os quatro scores de valoração, o IVC, o IAC, o INV e o quadrante.

---

## Estrutura de dados (`DADOS_MAPA`)

Todo o mapa é alimentado por uma única constante JavaScript, `DADOS_MAPA`, embutida em `index.html`:

```js
DADOS_MAPA = {
  dados: {            // 21 microrregiões, chave = código IBGE (ex.: "21001")
    "21001": {
      nome, num, micro_id,
      ind: { pop, area, densidade, pct_rural, cob_flor, desmat, gini,
             pct_agrifam, n_cat_col, pct_area_col, n_prod_ext,
             ivs, ivs_ch, idhm, pib_pc, pct_pobreza,
             ips_geral, ips_nhb, ips_conhec, ips_infocom,
             pop_serie, pib_pc_serie, pct_rural_serie },  // séries {"2010":.., "2022":..}
      val: { objetiva, percebida, social, potencial },     // cada um com {score, parts:[{label,raw,norm}]}
      ivc, iac, inv, classe_apt, classe_nec, quadrante,
      qualidade: { camposReais:[...], camposEstimativaAtlas2025:[...], atualizadoEm }
    }, ...
  },
  geo: { /* FeatureCollection GeoJSON com o polígono real das 21 microrregiões */ },
  comunidades: [        // 141 registros — ver tabela acima
    { id, tipo, nome, micro_id, micro_nome, centro:[lat,lon],
      geometria: /* GeoJSON ou null */, raio_m /* só quando geometria é null */,
      detalhes: {...}, fonte, ano_fonte }
  ],
  meta: { atualizadoEm, versao, nota }
}
```

---

## Módulos da plataforma (visão geral)

1. **Diagnóstico & linha de base** — ISA, avaliação ex ante, 12 dimensões territoriais, IVCT inicial.
2. **Desenho participativo** — tecnologias sociais, co-desenho com a comunidade.
3. **Execução & aprendizagem** — ciclos de teste, oficinas de avaliação participativa.
4. **Visualizações** — este mapa dinâmico, séries históricas, diagnósticos, painéis (BI).
5–8. Governança, portfólio, decisão e monitoramento contínuo (ver abas do site).

## Metodologia de valoração (resumo)

Quatro valorações (0–100) por território, todas por normalização min-max entre as 21 microrregiões:

- **Objetiva** — ativos verificáveis (cobertura florestal, IDHM, PIB per capita, sociobiodiversidade, IPS geral).
- **Percebida** — proxy de bem-estar (componentes do IPS + IVS invertido) até haver pesquisa de campo.
- **Social** — reconhecimento fundiário coletivo e agricultura familiar.
- **Potencial (= IAC)** — capacidade prospectiva de gerar inovação social.

A priorização cruza **IAC** (aptidão) × **INV** (necessidade, composto por desmatamento, Gini, IVS, IDHM invertido, PIB invertido, % pobreza e IPS-necessidades invertido) numa matriz 2×2 dividida pela mediana das 21 microrregiões. Detalhes completos, com a lista exata de componentes e pesos, estão na aba "Como os índices são determinados" do site.

## Limitações conhecidas

- Os índices compostos combinam, nesta rodada, indicadores com anos-fonte diferentes (2010 a 2023) — cada um está rotulado com seu ano real na interface, mas isso significa que o "retrato" de cada território não é de um único ano.
- A malha de comunidades (141 registros) é a mais completa que pôde ser verificada com fontes oficiais abertas nesta rodada; não é exaustiva de todos os povoados informais do estado (ver seção acima).
- As coordenadas dos distritos/povoados sem demarcação oficial são aproximadas (geocodificação por nome via OpenStreetMap), não uma medição de campo.

## Licença e créditos

Modelo conceitual demonstrativo, baseado na proposta PVCIST (Embrapa Maranhão). Dados de terceiros usados sob suas respectivas licenças/termos de uso público: IBGE, FUNAI, ICMBio, INCRA, MapBiomas, IPEA, Atlas Brasil/PNUD, Imazon, OpenStreetMap.
