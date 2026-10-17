# Healthcare Intelligence Monitor

**Monitor Contínuo de Inteligência em Saúde** - Adaptado de `always-on-agents`

## 🎯 Propósito

Monitoramento automático de fontes médicas e tecnológicas críticas para saúde no Brasil e globalmente.

## 🏗️ Arquitetura

```
healthcare_intelligence_monitor/
├── monitor_agent.py            # Agente principal
├── feeds/
│   ├── anvisa_feed.py        # ATMS ANVISA
│   ├── pubmed_feed.py        # Alertas PubMed
│   ├── hl7_feed.py          # Especificações HL7
│   └── fhir_feed.py         # FHIR Releases
├── config/
│   └── sources.yaml          # Fonte de dados
├── alerts/
│   └── create_alert.py
└── README.md
```

## 📡 Fontes Monitoradas

1. **ANVISA** - Alertas de farmacos, notificacoes, ATMS
2. **Ministério da Saúde** - Portarias, guias, atualizacoes
3. **PubMed** - Artigos sobre saúde pública, clínica
4. **HL7/FHIR** - Updates de especificações
5. **GitHub** - Repositorios médicos relevantes
6. **WHO** - Guidelines internacionais

## 🔄 Fluxo de Monitoramento

```
Scheduler (hourly)
    ↓
Fetch Sources
    ↓
Parse & Extract
    ↓
Classify (update/alert/norma)
    ↓
Filter (novo/relevante)
    ↓
Generate Brief
    ↓
Slack/Email Alert
```

## 📋 Formato de Alerta

```markdown
🆕 **NOVA ATUALIZAÇÃO** - ANVISA 2023-XXX

**Fonte:** Portaria ANVISA nº XXX/2023
**Tema:** Novo regulamento para medicamentos de alto custo
**Impacto:** Mudança na burocracia para fornecimento hospitalar

**Principais alterações:**
- Nova categoria de "medicamento de terapia única"
- Requisitos de documentação simplificados
- Prazo de 90 dias para adequação

**Ação recomendada:** Revisar portfólio de medicamentos
```

## ⚙️ Configuração

```yaml
# sources.yaml
sources:
  - name: "ANVISA ATMS"
    type: "rss"
    url: "https://www.gov.br/anvisa/pt-br/assuntos/noticias/rss.xml"
    keywords: ["medicamento", "regulamento", "portaria"]
    frequency: "hourly"
  
  - name: "PubMed Alerts"
    type: "api"
    keywords: ["hipertensão", "diabetes", "terapia"]
    frequency: "daily"
```

## 📊 Métricas

- Número de notícias processadas/dia
- Taxa de alertas relevantes
- Tempo de resposta
- Cobertura de fontes

## 🚀 Execução

```bash
python monitor_agent.py --config sources.yaml --output alerts/
```