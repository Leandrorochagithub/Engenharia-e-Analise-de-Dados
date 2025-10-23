# Projeto de Análise de Divergência de Inventário com Power BI

## 📊 Visão Geral do Projeto
Este projeto demonstra a aplicação de conceitos avançados de Engenharia de Dados no Power BI, transformando uma estrutura de dados centralizada e monolítica em um modelo dimensional otimizado (Star Schema). O foco principal é a análise de divergências de inventário em uma rede de farmácias.

**Antes / Depois**

<img width="400" height="200" alt="relacionamentosAntes" src="https://github.com/user-attachments/assets/f4e6a453-0bf6-43d6-b217-29892c9a2163" /> <img width="400" height="200" alt="relacionamentoDepois" src="https://github.com/user-attachments/assets/6453ff2b-90ff-454f-97b9-ebee9717401d" />


## 🏆 Prova de Performance: Otimização Mensurável

A migração de uma tabela única para um modelo Star Schema não foi apenas uma boa prática, foi uma necessidade de performance. Utilizei o **Analisador de Desempenho** do Power BI para medir o impacto da otimização.

**Os resultados são claros:**

* **Carregamento do Visual Principal (Tabela):**
    * **Antes:** 4.935 ms
    * **Depois:** 60 ms
    * **Resultado: 98,8% de redução** no tempo de consulta DAX.

* **Interatividade (Seleção de Filtro):**
    * **Antes:** 216 ms
    * **Depois:** 55 ms
    * **Resultado: 74,5% de melhoria** na responsividade do filtro.

Essa otimização transformou um relatório lento em uma ferramenta de análise rápida e viável para o uso diário.

<img width="500" height="350" alt="grafico_performance" src="https://github.com/user-attachments/assets/0fe5f3de-9afb-401a-a2cc-d69ed1f35147" />

Os dados brutos `.json` usados para esta análise estão disponíveis na pasta `/performance-data`.

## 🔄 Processo de Transformação de Dados
Antes da modelagem, todos os dados estavam centralizados em uma única tabela com múltiplos JOINs aninhados diretamente na query principal. 

![antesMonolitica](https://github.com/user-attachments/assets/bbd20127-e5b8-44c8-856b-c2a4277060f8)

**Isso causava:** 

* Baixa performance no carregamento e atualização dos dados
* Dificuldade de manutenção e debugging
* Reprocessamento desnecessário de dados a cada atualização
* Complexidade elevada na criação de relacionamentos

Para solucionar isso, foi realizado um processo completo de ETL (Extração, Transformação e Carga) diretamente no Power Query (Linguagem M) para modelar os dados em um **Esquema Estrela (Star Schema)**.

## 🏗️ Arquitetura Implementada
### 1. Camada Staging (STG)
**Tabelas intermediárias para preparação e limpeza dos dados:**
* stg_tb_inventario_contado - Dados brutos do inventário contado
* stg_f_inventario_inicial_limpo - Estoque inicial processado
* stg_f_inventario_contado_limpo - Estoque contado processado

#### Benefícios:
* Separação de responsabilidades
* Facilita debugging e validação
* Permite reuso de transformações

### 2. Tabelas Dimensionais (Modelo Star Schema)
![depoisDimensoes](https://github.com/user-attachments/assets/579b9143-ba10-4785-9256-f76fc8d5af1b)

**d_produto - Dimensão de Produtos**
* Chave primária: COD INTERNO
* Tratamento de códigos de barras ausentes
* Criação de chave concatenada: COD-PRODUTO (código + descrição)
* Normalização de texto (Text.Proper)

**d_filial - Dimensão de Filiais** 
* Chave primária: FILIAL - NUMERO
* Campos descritivos: número, texto e apelido
* Chave concatenada: FILIAL-APELIDO para melhor visualização

**d_ciclo - Dimensão de Ciclos de Inventário** 
* Chave primária: ID INVENTARIO
* Campos temporais: ANO, MES, DATA
* Campos descritivos: CICLO-DESCRITIVO (ex: "1° Ciclo")
* Removidas duplicatas por ID de inventário

**d_calendario - Dimensão Temporal**
* Gerada dinamicamente baseada no range de datas dos dados

**Colunas úteis:**
* Ano, Mês, Dia, Trimestre
* Nome do mês, mês abreviado
* Dia da semana, semana do ano
* AnoMesNumero (para ordenação correta)
* AnoMesTexto (formato visual)

### 3. Tabelas Fato
![depoisFatos](https://github.com/user-attachments/assets/6bc10e16-0ad4-4639-ba9c-5b00f1ba9988)

**f_inventario - Fato Principal**

**- Combina dois eventos de inventário:**
* Estoque Inicial (baseline)
* Estoque Contado (resultado da contagem física)


**Estrutura:**

- ID INVENTARIO
- COD INTERNO
- CUSTO UNITARIO (dividido por 100)
- QUANTIDADE
- TIPO EVENTO

**f_inventario_divergencias - Análise de Divergências** 

**- Tabela analítica resultante do Full Outer Join entre inicial e contado:**

**Métricas Calculadas:**

* DIF_QTD = Quantidade Contada - Quantidade Inicial
* DIF_VALOR = Diferença de Quantidade × Custo Unitário
* TIPO_DIVERGENCIA:
	- "falta" (DIF_QTD < 0)
	- "sobra" (DIF_QTD > 0)
	- "sem divergencia" (DIF_QTD = 0)


**Regra de Negócio:** Utiliza custo inicial quando disponível, senão custo contado

* f_produto_sem_cadastro - Produtos Não Cadastrados
	- Identifica produtos contados mas sem registro no cadastro principal:
	- Útil para auditoria e correção de dados
	- Flag: STATUS PRODUTO = "Sem cadastro"

## 🛠️ Técnicas de Power Query Aplicadas

**1. Tratamento de Dados** 

* m Substituição de valores nulos
Table.ReplaceValue(null, 0, Replacer.ReplaceValue, {"COLUNA"})

* Normalização de texto
Table.TransformColumns({{"COLUNA", Text.Proper, type text}})
* Divisão de valores (centavos para reais)
Table.TransformColumns({{"CUSTO", each _ / 100, type number}})

**2. Joins e Relacionamentos**
* LeftOuter Join: Para manter todos os registros da tabela principal
* FullOuter Join: Para capturar divergências entre inicial e contado
* Uso de Table.NestedJoin seguido de Table.ExpandTableColumn

**3. Criação de Colunas Customizadas**

* m Condicional para código de barras
	- if [COD BARRAS ORIGINAL] = null or [COD BARRAS ORIGINAL] = 0 then [COD INTERNO] else [COD BARRAS ORIGINAL]

* Classificação de divergências
	- if [DIF_QTD] < 0 then "falta" else if [DIF_QTD] > 0 then "sobra" else "sem divergencia"

**4. Geração Dinâmica de Calendário**
* m DataInicial = List.Min(d_ciclo[DATA])
* DataFinal = List.Max(d_ciclo[DATA])
* Duracao = Duration.Days(DataFinal - DataInicial) + 1
* ListaDeDatas = List.Dates(DataInicial, Duracao, #duration(1, 0, 0, 0))

## 📈 Benefícios da Nova Arquitetura
### Performance
⚡ Redução significativa no tempo de carregamento

🔄 Atualização incremental facilitada

💾 Otimização de memória e processamento

### Manutenibilidade
🔍 Queries modulares e mais legíveis

🐛 Debugging simplificado por camadas

📝 Documentação implícita pela estrutura

### Escalabilidade
➕ Fácil adição de novas dimensões

🔗 Relacionamentos claros e consistentes

📊 Suporte a análises complexas

### Governança
✅ Rastreabilidade de transformações

🎯 Separação de responsabilidades (staging/dimensões/fatos)

🔐 Validação de dados em múltiplas camadas


## 🎯 Casos de Uso Analítico
* **Análise de Perdas e Sobras:** Identificação de padrões de divergência por produto, filial e período
* **Acuracidade de Inventário:** Percentual de produtos sem divergência
* **Impacto Financeiro:** Valor monetário das divergências
* **Produtos Críticos:** Itens com maior frequência de divergência
* **Performance por Filial:** Comparativo de acuracidade entre lojas
* **Tendências Temporais:** Evolução das divergências ao longo dos ciclos

## 🔑 Conceitos de Engenharia de Dados Aplicados
✅ Star Schema (Modelagem Dimensional)

✅ ETL/ELT (Extract, Transform, Load)

✅ Staging Area (Camada intermediária)

✅ Data Quality (Tratamento de nulos, duplicatas, normalização)

✅ Slowly Changing Dimensions (Histórico temporal)

✅ Fact Table (Granularidade de eventos)

✅ Data Lineage (Rastreabilidade de transformações)

# 📝 Conclusão
Este projeto demonstra a aplicação prática de **Engenharia de Dados no contexto de Business Intelligence**, transformando dados brutos em um modelo analítico robusto, performático e escalável. A migração de uma estrutura monolítica para um Star Schema representa um ganho significativo em termos de performance, manutenibilidade e capacidade analítica.

**Tecnologias:** Power BI | Power Query (M) | DAX | Data Modeling

**Conceitos:** ETL | Star Schema | Data Quality | Dimensional Modeling

**Acesse o Dashboard Interativo** 

https://app.powerbi.com/view?r=eyJrIjoiYmRjYjRjY2MtN2E3Yi00Yjk1LWI4ZTgtYjNiNzZjMzkwMDExIiwidCI6ImYyOWVkNTkxLTBlNzAtNDQ5ZC05NDU3LTViZTBjNjQwYWY5NSJ9
