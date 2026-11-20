# Design Brief — Modernização Híbrida AON 2024

```yaml
Design Brief:
  generated_by: powerbi-report-cli
  contract_version: 1
  mode: brownfield
  design_identity:
    tone: "Executive Precision — alta legibilidade, contraste WCAG AA, paleta limpa e ausência total de chartjunk"
    signature: "Painel executivo em tela única com KPI-strip contextual, cartões com cantos arredondados de 8px e divisões suaves"
    current_tone: "Stacking denso com rolagem vertical excessiva (2.350px a 2.850px) e caixas cinzas pesadas"
    current_signature: "Rolagem contínua com repetição de 5 camadas visuais por página"
  palette:
    primary: "#0F1934"     # Azul Marinho Profundo (Corporate Header & Accent)
    secondary: "#457DFF"   # Azul Cobalto (Hero & Tendência)
    success: "#00B867"     # Verde Esmeralda (Conversões & Desempenho Positivo)
    warning: "#FFA200"     # Âmbar (Atenção / CPA Alto)
    neutral_bg: "#F9FAFC"  # Fundo Canvas Ultra-Leve
    card_bg: "#FFFFFF"     # Superfície de Cartões
    border: "#E2E8F0"      # Borda Sutil Slate-200 (8px radius)
    text_primary: "#1E293B" # Slate-800 para texto principal
    text_muted: "#64748B"   # Slate-500 para legendas e labels
  color_map:
    Investimento: "#0F1934"
    Conversões: "#00B867"
    CPA: "#FFA200"
    CTR: "#457DFF"
    Cliques: "#1443F6"
    Impressões: "#94A3B8"
  typography:
    family: "Segoe UI Variable, Segoe UI, sans-serif"
    callout_size: 26
    title_size: 14
    body_size: 10
  pages:
    - id: "068c7c558f484bd8f2cd"
      name: "Visão Geral"
      archetype: "Executive Summary"
      layout_variant: "Hero-Right"
      canvas:
        width: 1500
        height: 844  # 16:9 Zero-Scroll (reduzido de 2.350px)
      zones:
        header:
          height: 70
          elements: ["Logotipo", "Título da Página", "Filtros Globais (Ano, Mês, Canal)"]
        kpi_strip:
          height: 130
          cards: ["Investimento Total", "Conversões", "CPA Geral", "Taxa de Conversão", "CTR"]
        main_analytics:
          height: 380
          left_hero: "Evolução Temporal de Investimento vs Conversões (Line/Bar Chart)"
          right_ranking: "Top Canais / Veículos por Eficiência (Clustered Bar Chart)"
        detail_summary:
          height: 220
          left_matrix: "Matriz Resumo por Plataforma (Meta vs Google vs Outros)"
          right_creatives: "Top 5 Criativos com Melhor Performance (Tabela com nome higienizado)"
        footer:
          height: 34
          elements: ["Data de Atualização", "Botões de Navegação Aprofundada para Canais"]
    - id: "81d79a9785f5a0b4f04a"
      name: "CPM"
      archetype: "Analytical Canvas"
      canvas:
        width: 1500
        height: 1000  # Reduzido de 2.280px para navegação focada
    - id: "6a9980cf8283277cff5b"
      name: "CPV"
      archetype: "Analytical Canvas"
      canvas:
        width: 1500
        height: 1000  # Reduzido de 2.850px
    - id: "1fb851229a0f81b49aef"
      name: "CPC"
      archetype: "Analytical Canvas"
      canvas:
        width: 1500
        height: 1000  # Reduzido de 2.300px
```
