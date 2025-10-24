# 📊 Dashboard de Produtividade de Inventário - Power BI

## Análise de Performance Operacional em Rede de Farmácias

---

## 🎯 Visão Geral do Projeto

Dashboard analítico desenvolvido em **Power BI** para monitoramento e otimização da **produtividade operacional** em inventários. O projeto abrange três dimensões principais de análise: **performance das lojas**, **produtividade individual dos colaboradores** e **estatísticas detalhadas de produção**.

**Período de Análise:** Janeiro a Dezembro de 2024  
**Última Atualização:** 24/10/2025 10:46:07  
**Último Inventário:** 20/03/2025

---

## 📱 Estrutura do Dashboard

### **Página 1: Produtividade das Lojas**
*Visão gerencial e estratégica do desempenho por unidade*

#### 🔑 KPIs Principais

| Métrica | Valor | Descrição |
|---------|-------|-----------|
| **Total de Estoque Contado** | 33.396.797 itens | Volume total de produtos inventariados |
| **Média de Estoque Contado** | 44.234 itens/loja | Capacidade média operacional por unidade |
| **Média de Inventariantes** | 9 colaboradores/loja | Tamanho médio das equipes |

#### 📊 Análises Visuais

**1. Ranking de Empresas (Top 5)**
```
Droga C    → 193 inventários
Droga F    → 172 inventários
Droga Bb   → 98 inventários
Droga D    → 71 inventários
Droga G    → 66 inventários
```
*Insight: Droga C lidera em volume operacional, representando maior participação no portfólio*

**2. Timeline de Contagem Mensal**
- **Pico de Atividade:** Fevereiro (4.459.727 itens)
- **Menor Atividade:** Agosto (1.780.985 itens)
- **Sazonalidade:** Concentração maior no 1º trimestre

**3. Detalhamento por Empresa**
Tabela com dados de estoque contado e data do último inventário para cada rede parceira

#### 🎛️ Filtros Interativos
- Ano | Empresa | Ciclo | Filial | Regional | Mês | Dia

---

### **Página 2: Produtividade dos Funcionários**
*Análise de performance individual e gestão de equipes*

#### 🏆 Top Performers

| Posição | Nome | Média Contagem | Média Anterior | Evolução |
|---------|------|----------------|----------------|----------|
| 1º | Renato Rodrigues Dos Santos | 10.767 | 10.744 | ↗️ +23 |
| 2º | Leticia Cibele | 10.734 | 10.489 | ↗️ +245 |
| 3º | Jose Demerival Das Santos | 9.841 | 8.976 | ↗️ +865 |
| 4º | Elias Lopes | 8.603 | 8.310 | ↗️ +293 |
| 5º | Mayara Oliveira Da Rocha | 8.553 | 8.174 | ↗️ +379 |

*Insight: Top performers apresentam crescimento consistente, indicando curva de aprendizado positiva*

#### 📈 Métricas Consolidadas

| Indicador | Valor |
|-----------|-------|
| **Total Contado** | 32.065.295 itens |
| **Média de Contagem** | 4.866 itens/colaborador |
| **Mediana** | 4.339 itens |
| **Total de Correções** | 11.676 erros |

#### 🎯 Sistema de Gamificação - Níveis de Performance

```
💎 Diamante → 12.000 itens
🏆 Platina  → 8.250 itens
🥇 Ouro     → 5.500 itens
🥈 Prata    → 4.500 itens (Nível Atual)
🥉 Bronze   → 3.500 itens
⚪ Cobre    → 2.500 itens
```

**Meta Atual:** 5.500 itens (Nível Ouro)  
**Progresso para Próximo Nível:** 88,48%

#### 📊 Gráfico de Tendência Mensal
Visualização da evolução da contagem média ao longo do ano com identificação de erros:
- **Melhor Mês:** Maio (5.296 itens | 2 erros médios)
- **Performance Consistente:** Médias entre 4.500-5.500 itens
- **Controle de Qualidade:** Média de 2 erros por colaborador/mês

#### 🎛️ Filtros Interativos
- Ano | Mês | Dia | Nome | Regional | Conformidade

---

### **Página 3: Estatísticas de Produção**
*Deep dive em qualidade, conformidade e demografia operacional*

#### 📋 Tabela Detalhada de Registros
Granularidade máxima com informações por operação:
- Data | Mês | Chave (Empresa) | Nome do Colaborador
- Contagem Individual | Número de Erros | Status de Conformidade

**Exemplo de Registro:**
```
Data: 03/01/2024
Empresa: Droga C (Filial 5)
Colaborador: Deivi Moraes
Contagem: 11.118 itens
Erros: 5
Conformidade: Multiplo
```

#### 🎯 Indicadores de Qualidade

| Métrica | Valor | Análise |
|---------|-------|---------|
| **Qualidade da Contagem** | 99,96% | Excelente acuracidade operacional |
| **Total de Correções** | 11.676 | Sobre 32M+ itens contados |
| **Taxa de Erro** | 0,04% | Benchmark de classe mundial |

#### 👥 Análise Demográfica da Força de Trabalho

**Distribuição por Gênero:**
- 👨 Homens: 121 colaboradores (59,0%)
- 👩 Mulheres: 84 colaboradoras (41,0%)
- **Total:** 205 colaboradores ativos

**Análise de Mobilidade:**
- 🏠 **Moradia Próxima (<40km):** 197 colaboradores (96,1%)
- 🚗 **Moradia Distante (+40km):** 8 colaboradores (3,9%)

*Insight: 96% da equipe mora próximo aos locais de trabalho, otimizando pontualidade e reduzindo custos de deslocamento*

#### 🏅 Classificação de Conformidade
- **"Multiplo":** Colaborador opera com contagem múltiplas de unidades
- **"Nao Multiplo":** Colaborador opera com contagem unitária

#### 🎛️ Filtros Interativos
- Ano | Mês | Dia | Usuário | Conformidade

---

## 🎨 Design e Experiência do Usuário

### **Identidade Visual**
- **Paleta de Cores:** Tons de azul e laranja (contraste profissional)
- **Tipografia:** Fonte clara e legível, hierarquia bem definida
- **Layout:** Grid organizado com cards de KPIs em destaque

### **Navegação**
- **Páginas numeradas:** 1, 2, 3 (indicadores visuais de posição)
- **Filtros globais:** Sincronização entre páginas
- **Timestamp:** Data/hora da última atualização sempre visível

### **Interatividade**
- ✅ Slicers para segmentação dinâmica
- ✅ Drill-through entre páginas
- ✅ Tooltips informativos
- ✅ Ordenação inteligente de rankings

---

## 💡 Principais Insights Analíticos

### 📈 **Performance Operacional**
1. **Volume Impressionante:** 33+ milhões de itens inventariados demonstram escala operacional robusta
2. **Consistência:** Média de 9 inventariantes por loja garante cobertura adequada
3. **Sazonalidade:** 1º trimestre apresenta maior atividade (possível planejamento fiscal/anual)

### 👤 **Gestão de Pessoas**
1. **Top Performers:** Colaboradores de destaque com produtividade 2x acima da média
2. **Gamificação Efetiva:** Sistema de níveis incentiva melhoria contínua (88% para próximo nível)
3. **Curva de Aprendizado:** Comparação mês anterior mostra evolução positiva

### 🎯 **Qualidade**
1. **Excelência Operacional:** 99,96% de acuracidade é benchmark de mercado
2. **Controle de Erros:** Apenas 11.676 correções em 32M+ itens (0,04%)
3. **Conformidade Alta:** Sistema identifica e monitora desvios

### 🌍 **Logística**
1. **Otimização Geográfica:** 96% da equipe mora próximo (reduz turnover e atrasos)

---

## 🔧 Tecnologias e Recursos Utilizados

### **Power BI Features**
- ✅ **DAX Measures:** Cálculos complexos (médias, medianas, percentuais)
- ✅ **Bookmarks:** Navegação fluida entre páginas
- ✅ **Conditional Formatting:** Destaque de KPIs críticos
- ✅ **Custom Visuals:** Gráficos otimizados para storytelling
- ✅ **Drillthrough Pages:** Análise detalhada sob demanda

### **Modelagem de Dados**
- 📊 **Tabelas Fato:** Registros transacionais de inventário
- 📅 **Dimensão Temporal:** Calendário completo
- 👥 **Dimensão Colaborador:** Informações demográficas e performance
- 🏢 **Dimensão Empresa/Filial:** Hierarquia organizacional

---

## 📊 Casos de Uso e Aplicações

### **Para Gestores Operacionais:**
- Monitoramento em tempo real de produtividade por loja
- Identificação de filiais com baixa performance
- Planejamento de alocação de recursos

### **Para RH:**
- Gestão de talentos e identificação de high performers
- Programa de incentivos baseado em gamificação
- Análise de turnover e mobilidade

### **Para Diretoria:**
- Visão estratégica do volume operacional
- ROI de investimentos em equipes
- Benchmarking entre unidades de negócio

### **Para Controle de Qualidade:**
- Rastreamento de erros e não conformidades
- Identificação de padrões de falhas
- Ações corretivas direcionadas

---

## 🚀 Diferenciais do Projeto

✨ **Gamificação:** Sistema de níveis inovador que engaja colaboradores  
📊 **Visão 360°:** Do estratégico (loja) ao tático (colaborador)  
🎯 **Foco em Qualidade:** 99,96% de acuracidade demonstra excelência  
👥 **People Analytics:** Análise demográfica e de mobilidade integrada  
⚡ **Atualização em Tempo Real:** Timestamp visível garante confiabilidade  
🔄 **Comparação Temporal:** Métricas "anterior vs atual" mostram evolução

---

## 🎓 Aprendizados e Best Practices

### **Modelagem**
- Granularidade adequada (operação individual)
- Relacionamentos 1:N bem definidos

### **Performance**
- Agregações pré-calculadas para KPIs
- Filtros contextuais otimizados
- Carregamento incremental de dados

### **UX/UI**
- Cores acessíveis (contraste adequado)
- Hierarquia visual clara

---

## 📝 Conclusão

Este dashboard representa uma **solução completa de Business Intelligence** para gestão de operações de inventário, combinando:

- 📊 **Analytics Descritivo:** O que aconteceu?
- 🔍 **Analytics Diagnóstico:** Por que aconteceu?
- 🎯 **Analytics Prescritivo:** O que fazer?

A implementação de **gamificação**, **people analytics** e **controle de qualidade rigoroso** demonstra uma abordagem moderna e data-driven para gestão operacional, entregando valor tangível para todos os stakeholders do negócio.

---

**Tecnologias:** Power BI | DAX | Power Query (M) | Data Modeling  
**Competências:** Business Intelligence | Data Visualization | People Analytics | Operational Excellence

---

### 📌 Link do Dashboard
https://app.powerbi.com/view?r=eyJrIjoiMTFlYzFiNDEtZjk4Ni00YjM4LThlMDUtOTc2MzI0NjMwNjIyIiwidCI6ImYyOWVkNTkxLTBlNzAtNDQ5ZC05NDU3LTViZTBjNjQwYWY5NSJ9