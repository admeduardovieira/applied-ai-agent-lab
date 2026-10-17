# Arquitetura do Applied AI Agent Lab

## Visão Geral

Este laboratório implementa arquiteturas de agentes de IA adaptadas do projeto `awesome-llm-apps` para o domínio de saúde brasileira.

## Padrões de Arquitetura

### 1. Agent Design Pattern

Baseado em OpenAI Agents SDK:

```
┌─────────────────┐
│   User Input    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Planner       │ ◄── Define tasks and tools
└────────┬────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌───────┐ ┌─────────┐
│Tool 1 │ │Tool 2   │ ◄── External/API integrations
└──┬────┘ └────┬────┘
   │            │
   └─────┬──────┘
         ▼
┌─────────────────┐
│  Synthesizer    │ ◄── Combine results
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Output        │
└─────────────────┘
```

### 2. Safety Layer (Healthcare)

```
┌─────────────────┐
│   Input         │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Safety Filter  │ ◄── Check for PHI, unsafe content
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Processing    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Citation Gen   │ ◄── Source attribution (REQUIRED)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Output        │ ◄── Always with disclaimer
└─────────────────┘
```

### 3. Evidence Hierarchy

```
Level A ── Guidelines (SBP, NICE, WHO)
Level B ── RCTs (Randomised Controlled Trials)
Level C ── Observational Studies
Level D ── Case Reports/Expert Opinion
```

## Componentes Reusáveis

### Core Modules

| Module | Função | Baseado em |
|--------|--------|------------|
| `MedicalResearcher` | Busca evidências | ai-deep-research-agent |
| `FraudDetector` | Investigação de anomalias | ai-fraud-investigation-agent |
| `IntelligenceMonitor` | Monitoramento contínuo | always-on-agents |
| `GuidelineParser` | Extração de recomendações | custom |

### Data Sources

| Fonte | Tipo | Uso Principal |
|-------|------|---------------|
| PubMed/MedLine | Acadêmico | Evidências |
| SciELO Brasil | Acadêmico | Dados locais |
| CNES/CNPJ | Registro | Identificação |
| e-SIC/Legislação | Público | Conformidade |
| HL7/FHIR | Espec | Interop |

## Segurança e Compliance

1. **LGPD** - Never process personal health data
2. **ANVISA** - Only public regulatory info
3. **CLINICAL** - Never diagnose, only inform
4. **SOURCE** - Always cite primary sources

## Performance Targets

| Metra | Meta | Atual |
|-------|------|-------|
| Tempo de pesquisa | < 30s | - |
| Cobertura de fontes | > 85% | - |
| Precisão de dados | > 95% | - |
| Taxa de erro | < 2% | - |

---

*Documentação baseada em análise de awesome-llm-apps*
*Adaptado para saúde brasileira*