# @heritage/pharmaceutical-dataset

[![Version](https://img.shields.io/badge/version-v2026.09.27-blue.svg)](https://github.com/qeqsoftlab-code/pharmaceutical-dataset)
[![ANVISA](https://img.shields.io/badge/ANVISA-Dados%20Abertos-green.svg)](https://dados.anvisa.gov.br/)
[![WADA Season](https://img.shields.io/badge/WADA-Season%202026-red.svg)](https://www.wada-ama.org/)
[![License](https://img.shields.io/badge/license-UNLICENSED-lightgrey.svg)](LICENSE)

Repositório Canônico e Hub Central de Inteligência Farmacológica, Registros ANVISA e Conformidade Antidopagem WADA/ABCD 2026 para o ecossistema Heritage Power Pro.

---

## 🏛️ Arquitetura em Espelho

Mantém a simetria exata com os repositórios canônicos do ecossistema:
- `qeqsoftlab-code/nutrition-dataset` (dados nutricionais TACO enriquecida e catálogo de alimentos)
- `qeqsoftlab-code/exercises-dataset` (catálogo padronizado de exercícios e padrões biomecânicos)
- **`qeqsoftlab-code/pharmaceutical-dataset`** (catálogo farmacológico, DCB e antidoping)

### Pipeline Automatizado

1. **Ingestão dos Dados Abertos da ANVISA:**
   - Normalização a partir da base oficial `DADOS_ABERTOS_MEDICAMENTOS.csv`;
   - Resolução de homônimos e identificação de números de processo e registro sanitário brasileiro.

2. **Normalização Semântica & RxNorm:**
   - Mapeamento cruzado com códigos ATC da OMS e identificadores RxCUI da National Library of Medicine (NIH).

3. **Conformidade Antidoping WADA / ABCD 2026:**
   - Classificação estrita nas categorias S0 a S9 (esteroides anabólicos, agonistas beta-2, moduladores metabólicos, glicocorticoides);
   - Mapeamento informativo de redução de danos (harm reduction) e monitoramento laboratorial (hematócrito, enzimas hepáticas, perfil lipídico).

4. **Snapshot Canônico Versionado:**
   - Geração de arquivos leves com integridade garantida por SHA-256 e release tags `vYYYY.MM.DD`.

---

## 📁 Estrutura de Arquivos

```
qeqsoftlab-code/pharmaceutical-dataset/
├── .github/workflows/
│   └── validate-and-release.yml   # Validação de integridade JSON e geração de releases
├── data/
│   ├── metadata.json              # Versionamento, tag, checksum SHA-256 e timestamps
│   ├── anvisa-canonical.json      # Catálogo canônico de 24 fármacos de referência e princípios ativos
│   └── wada-2026-classes.json     # Classificação normativa WADA 2026 (S0 a S9, M1)
├── package.json                   # Pacote @heritage/pharmaceutical-dataset
├── README.md                      # Documentação técnica e de consumo
└── .gitignore                     # Filtros de arquivos ignorados
```

---

## 🚀 Consumo da API / Raw Release

Os clientes SaaS consomem o release oficial diretamente via HTTP:

- **Catálogo Canônico:**
  `https://raw.githubusercontent.com/qeqsoftlab-code/pharmaceutical-dataset/main/data/anvisa-canonical.json`
- **Metadados & Checksum:**
  `https://raw.githubusercontent.com/qeqsoftlab-code/pharmaceutical-dataset/main/data/metadata.json`
- **Classes WADA 2026:**
  `https://raw.githubusercontent.com/qeqsoftlab-code/pharmaceutical-dataset/main/data/wada-2026-classes.json`

---

## 🛡️ Validação & Qualidade de Dados

- **Idempotência Garantida:** Cada medicamento possui `slug` determinístico e chave única de registro ANVISA;
- **Semantização de Princípios Ativos:** Todos os fármacos vinculam-se a princípios ativos padronizados via DCB/ATC/RxCUI;
- **Auditoria de Checksum:** Consumidores verificam o hash SHA-256 antes do download para evitar transferências e reescritas desnecessárias (`SKIP`).
