# 📊 AON 2024 — Plataforma Consolidada de Inteligência de Mídia & Performance

[![Power BI](https://img.shields.io/badge/Power_BI-PBIP_Format-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Semantic Model](https://img.shields.io/badge/Model-TMDL_Standard-217346?logo=microsoft)](https://learn.microsoft.com/power-bi/transform-model/desktop-tmdl)
[![Quality Audit](https://img.shields.io/badge/Audit_Score-95.2%25_(Grade_A)-success)](AUDIT-REPORT.md)
[![Design System](https://img.shields.io/badge/Design-16%3A9_Zero--Scroll-0078D4)](_brief/redesign-brief.md)
[![Fabric Skills](https://img.shields.io/badge/Microsoft_Fabric-28_Official_Skills-7FBA00?logo=azure)](https://github.com/microsoft/skills-for-fabric)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Plataforma analítica e modelo semântico empresarial para consolidação, higienização e visualização de desempenho de campanhas de mídia digital (Meta Ads, Google Ads, GA4 e canais receptivos). 

Desenvolvido no formato oficial de desenvolvedor **Power BI Project (`.pbip`)** com separação modular entre modelo semântico (**TMDL**) e relatório (**PBIR**), permitindo controle de versão limpo, governança avançada e automação com agentes autônomos.

---

## 🌟 Destaques do Projeto

### 1. Auditoria e Governança de Dados (Nota A - 95.2%)
O modelo semântico foi auditado e refatorado com base nas melhores práticas mundiais de engenharia do Power BI:
- **Zero Auto Date/Time Bloat**: Desativação total de tabelas de data automáticas ocultas (`__PBI_TimeIntelligenceEnabled = 0`), eliminando overhead de memória e garantindo controle via `DATA_DIM` (`dataCategory: Time`).
- **Esquema Estrela Certificado**: Fatos analíticos limpos (`REDES_FATO`, `GA_FATO`, `GA_EVENTOS_FATO`) conectados às dimensões através de relacionamentos unidirecionais 1:* estritos.
- **Camada Semântica Segura**: Todas as divisões utilizam a função segura `DIVIDE()`, evitando erros de divisão por zero.
- **100% de Métricas e Tabelas Documentadas**: Documentação embutida no TMDL utilizando doc comments oficiais `///`.
- **Display Folders Estruturadas**: Todas as medidas de negócio organizadas em pastas visuais (`01. Custo e Investimento`, `02. Alcance e Impressões`, `03. Tráfego e Cliques`, `04. Conversões e Leads`).

### 2. Higienização Dimensional de Criativos
Pipeline de transformação em Power Query M (`fnSanitizarNome`) para padronização de dados:
- Higienização automática de nomes de anúncios: remoção de tokens de tracking `(naugm...)`, parênteses técnicos, identificadores de veiculação e sufixos de resolução (`1080x1080`, `1200x628`).
- **Integridade Relacional Preservada**: A coluna bruta original `Promoted post name` permanece como chave oculta de junção (`isHidden`), enquanto a nova dimensão `Criativo` é exposta aos usuários em formato limpo e legível.

### 3. Design System & UX de Elite (`powerbi-report-cli`)
Estrutura visual modernizada de acordo com o framework de design de produtos da Microsoft:
- **Visão Geral em Tela Única (Zero-Scroll 16:9)**: Canvas padronizado em 1500x844px baseado no arquétipo *Executive Summary*. Elimina a rolagem vertical de 2.350px e agrupa:
  - Header institucional e segmentadores contextuais (Período, Veículo, Tipo de Compra);
  - KPI Strip com os 5 principais indicadores executivos;
  - Hero Chart de evolução temporal por semana e gráficos de dispersão/colunas de eficiência;
  - Matriz de plataformas e tabela de criativos higienizados lado a lado.
- **Tema Corporativo Acessível**: Paleta de alto contraste aderente às normas **WCAG AA**, bordas com raio de 8px e ausência de sombras ou caixas cinzas pesadas.
- **Páginas Táticas Dedicadas**: Aprofundamento por objetivo de mídia (*CPM*, *CPV*, *CPC* e *Receptivo*).
- **One Page Mobile**: Visualização vertical otimizada para smartphones e executivos em trânsito.

### 4. Inteligência com Agentes do Microsoft Fabric
O projeto integra nativamente o catálogo oficial com **28 skills e agentes do Microsoft Fabric** em [`.agents/`](.agents/), incluindo:
- `powerbi-report-cli` & `semantic-model-authoring` para governança contínua;
- `e2e-medallion-architecture` para transição para Lakehouse/OneLake;
- `activator-cli` para alertas proativos em tempo real via Reflex (Teams/Email);
- Personas prontas para orquestração: `FabricAdmin`, `FabricDataEngineer` e `FabricIQ`.

---

## 📁 Estrutura do Repositório

```text
├── AON_2024.pbip                  # Arquivo mestre do Power BI Project
├── AON_2024.Report/               # Definição do Relatório (PBIR)
│   ├── definition/
│   │   ├── report.json            # Configurações do relatório e tema
│   │   └── pages/                 # Páginas e visuais do relatório
│   │       ├── 068c7c558f484bd8f2cd/  # Visão Geral (Painel Executivo 16:9)
│   │       ├── 1fb851229a0f81b49aef/  # CPC (Tráfego e Cliques)
│   │       ├── 6a9980cf8283277cff5b/  # CPV (Visualizações de Vídeo)
│   │       ├── 81d79a9785f5a0b4f04a/  # CPM (Alcance e Impressões)
│   │       ├── 3ad57981c7d7683706f3/  # Receptivo (Canais e Conversões)
│   │       ├── 386e075eae2f0120abde/  # Estratégia
│   │       ├── 80aecfbed9e249c02bf3/  # Menu Institucional
│   │       └── 5eb9f95cce88ea360b45/  # One Page Mobile
│   └── StaticResources/          # Imagens institucionais e temas
├── AON_2024.SemanticModel/        # Modelo Semântico (TMDL)
│   └── definition/
│       ├── database.tmdl          # Propriedades do banco de dados
│       ├── model.tmdl             # Estrutura do modelo e relacionamentos
│       ├── expressions.tmdl       # Consultas M e funções de higienização
│       └── tables/                # Tabelas Fato e Dimensões em TMDL
├── .agents/                       # Catálogo Oficial de Skills e Agentes Fabric
│   ├── skills/                    # 37 Skills corporativas (PBIP, Fabric, Lakehouse)
│   ├── agents/                    # Personas de agentes especialistas
│   └── common/                    # Guias de engenharia e referências CLI
├── _brief/                        # Especificações técnicas e briefs de design
├── AUDIT-REPORT.md                # Relatório completo da auditoria do modelo
├── historia-do-modelo.html        # Site interativo com a linha do tempo do projeto
└── README.md                      # Documentação do projeto
```

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
- **Windows 10/11**
- **Power BI Desktop** (versão mais recente com suporte a **PBIP** ativado em *Opções > Recursos de Visualização Prévia > Opção de Salvamento de Projeto do Power BI (.pbip)*)
- **Git** (para controle de versão)

### Passos
1. Clone o repositório:
   ```bash
   git clone https://github.com/rdsmelobsb/aon-pbi-report.git
   cd aon-pbi-report
   ```
2. Abra o arquivo executável do projeto:
   - Dê um duplo clique em **`AON_2024.pbip`**
3. O Power BI Desktop carregará instantaneamente a definição do modelo a partir do TMDL e o relatório a partir do PBIR.

---

## 📖 Documentação Adicional
- 📜 [AUDIT-REPORT.md](AUDIT-REPORT.md): Relatório detalhado dos 25 testes de modelagem, segurança e performance.
- 🎨 [_brief/redesign-brief.md](_brief/redesign-brief.md): Especificação das diretrizes e contratos de UX/Design.
- 🌐 [historia-do-modelo.html](historia-do-modelo.html): Apresentação interativa da linha do tempo da arquitetura (2024–2026).

---

## 📄 Licença
Distribuído sob a licença **MIT**. Consulte `LICENSE` para mais informações.
