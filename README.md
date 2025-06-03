# Projeto de Análise Exploratória de Dados (EDA)

## Sumário

- [Introdução](#introdução)  
- [Objetivo](#objetivo)  
- [Fontes de Dados](#fontes-de-dados)  
- [Metodologia](#metodologia)  
- [Desenvolvimento](#desenvolvimento)  
- [Conclusão](#conclusão)  
- [Referências](#referências)  

---

## Integrantes

- Nome: Erick Eiji Nagao                Ra: 21.00690-3  
- Nome: Igor Improta Martinez da Silva  Ra: 21.00834-5  
- Nome: Gabriel Henrique Baca Rado      Ra: 21.01286-5  
- Nome: Ryuske Hideaki Sato             Ra: 21.00745-4  
- Nome: Vinicius de Oliveira Berti      Ra: 21.01219-9  

---

## Introdução

Crises econômicas têm impactos que vão muito além de indicadores como PIB ou inflação. Elas afetam diretamente a vida das pessoas, e esse reflexo também aparece na saúde mental da população. O suicídio, infelizmente, é um dos indicadores mais extremos desse sofrimento.

Segundo dados da Organização Mundial da Saúde (WHO), a média global de suicídios em 2021 foi de aproximadamente 9,0 por 100 mil habitantes. No Brasil, essa taxa foi ligeiramente inferior (∼7,5 por 100 mil), mas o crescimento entre 2019 e 2020 foi alarmante: aumento de 13%.

Durante o mesmo período, o país enfrentou crises econômicas marcantes, como a de 2015 e os efeitos da pandemia em 2020. A taxa de desemprego chegou a 13,9% em 2020 (IBGE), e o PIB per capita caiu significativamente.

Por que escolhemos este tema? Porque acreditamos que políticas econômicas devem considerar também seus efeitos sobre a saúde mental da população. Com o acesso a dados públicos via APIs da WHO e do World Bank, buscamos explorar essas relações de forma quantitativa, destacando padrões, tendências e desigualdades que merecem atenção.

---

## Objetivo

Investigar a relação entre variáveis econômicas — como desemprego e PIB per capita — e a taxa de suicídio no Brasil entre 2013 e 2021 (último ano com dados disponíveis). Através de uma análise exploratória rigorosa e visualmente clara, buscamos evidenciar os efeitos sociais das crises econômicas sobre a saúde mental da população.

---

## Fontes de Dados

- **WHO (World Health Organization)**  
  - Taxa de suicídio anual (por 100 mil habitantes), global e Brasil, de 2000 a 2021.  
- **World Bank Open Data**  
  - PIB per capita (US$) anual do Brasil, 2013–2023.  
  - Taxa de desemprego anual do Brasil, 2013–2023.  

---

## Metodologia

1. **Coleta de dados via APIs**  
   - Utilizamos a API da WHO para baixar a série histórica de suicídio (2000–2021).  
   - Utilizamos a API do World Bank para obter PIB per capita e desemprego (2013–2023).  
   - Consultamos o IBGE para validar valores de desemprego e coletamos índices de inflação anuais (IPCA).

2. **Pré-processamento e normalização dos dados**  
   - Ajustamos nomes de colunas para padronização (`ano`, `taxa_suicídio`, `sexo`, `desemprego`, `pib_per_capita`, `inflacao`).  
   - Convertimos o campo `ano` para formato numérico e ordenamos cronologicamente.  
   - Realizamos interpolação linear para preencher eventuais lacunas em séries anuais.  
   - Unimos todas as tabelas por chave `ano`, gerando um dataset consolidado de 2013 a 2023 com as variáveis de interesse.  

3. **Análises de tendências temporais**  
   - Construímos gráficos de linha para visualizar:  
     - **Taxa de suicídio global vs. Brasil (2000–2021)**.  
     - **Taxa de suicídio no Brasil por gênero (2000–2021 e 2013–2023)**.  
     - **Taxa de desemprego no Brasil (2013–2023)**.  
     - **PIB per capita no Brasil (2013–2023)**.  
     - **Desemprego × PIB per capita (gráfico combinado 2013–2023)**.  

4. **Testes estatísticos de hipótese e correlações**  
   - **Teste t** (ou ANOVA) para comparar médias de `taxa_suicídio` entre diferentes decênios.  
   - **Correlação de Pearson** entre:  
     - Desemprego e Taxa de suicídio (2013–2023).  
     - PIB per capita e Taxa de suicídio (2013–2023).  
   - Cálculo da **matriz de correlação** entre as variáveis `taxa_suicídio`, `desemprego`, `pib_per_capita` e `inflacao`.

5. **Visualizações com Matplotlib e Seaborn**  
   - Gráficos de linha, scatter plots com linhas de regressão, histogramas de resíduos e heatmap de correlação.  
   - Destaque de anos-chave (2015, 2017, 2020, 2021) em scatter plots anotados com rótulos.  

---

## Desenvolvimento

### Evolução da taxa de suicídio – Global vs. Brasil (2000–2021)
- Enquanto a média global caiu de 13,7 para 8,9 por 100 mil habitantes, o Brasil subiu de 4,7 para 7,0 no mesmo período. O ponto de inflexão ocorreu em 2014–2015, vinculando‐se à recessão econômica.

### Evolução da taxa de suicídio no Brasil por sexo (2000–2021)
- Homens passaram de 7,7 para 10,7 por 100 mil, e mulheres de 1,9 para 3,6. A razão homem:mulher caiu de ~4:1 para ~3:1, indicando maior crescimento relativo para o público feminino.

### Evolução da taxa de desemprego no Brasil (2013–2023)
- Desemprego caiu de 7,1% (2013) para 6,8% (2014), subiu a 12,8% (2017) pela recessão de 2015–2016, atingiu 13,7% em 2020 (pandemia) e recuou para 7,9% em 2023.

### Desemprego × PIB per capita no Brasil (2013–2023)
- Apesar de PIB per capita recuperar‐se em 2017 (US$ 10 350), o desemprego permaneceu alto (~12,8%), evidenciando defasagem. Em 2020, PIB caiu para US$ 7 100 e desemprego saltou a 13,7%. De 2021 a 2023, PIB voltou a US$ 10 250 e desemprego caiu para 7,9%.

### Relação entre PIB per capita e Desemprego (2013–2023)
- Correlação negativa forte (r ≈ –0,85): anos como 2017 e 2020 destacam‐se por defasagens e choques simultâneos. Em 2020, o ponto “PIB baixo, desemprego alto” foi extremo.

### Evolução da taxa de suicídio mundial (2013–2023)
- A taxa mundial caiu de ~10,12 para 8,89 entre 2013 e 2020, com leve alta a 8,90 em 2021. O Brasil seguiu trajetória oposta, reforçando que fatores internos pesaram mais que as tendências globais.

### Taxa de suicídio no Brasil por sexo (2013–2023)
- Homens: 8,9 → 10,6; mulheres: 2,6 → 3,6. A razão caiu de ~3,4:1 para ~3:1. Mesmo após 2021, a taxa feminina continuou em alta, refletindo sobrecarga e vulnerabilidades específicas.

### Taxa de desemprego no Brasil (2013–2023)
- Reforça o pico de 13,7% em 2020 e a rápida recuperação a 7,9% em 2023, em contraste com a defasagem pós‐2015, quando o desemprego permaneceu alto mesmo com leve recuperação de PIB.

### Desemprego × PIB per capita no Brasil (2013–2023)
- Confirma correlação inversa (r ≈ –0,82). Em 2017, PIB subiu a US$ 10 350 e desemprego manteve‐se alto, mostrando defasagem. Em 2020, choques simultâneos de PIB e desemprego reforçam correlação quase instantânea.

### Correlação – Desemprego vs. Taxa de suicídio (2013–2023)
- Correlação positiva forte (r ≈ +0,86). Em 2017 e 2021, a taxa de suicídio ficou acima do valor previsto pelo desemprego, indicando efeitos adicionais (recessão prolongada, pandemia).

### Correlação – PIB per capita vs. Taxa de suicídio (2013–2023)
- Correlação negativa moderada (r ≈ –0,68). Em 2017 e 2020–2021, a taxa de suicídio superou o valor previsto apenas pelo PIB, destacando impactos sociopsicológicos extraeconômicos.

### Matriz de correlação (2013–2023)
- Principais correlações:  
  - desemprego × suicídio_total = +0,86  
  - pib_per_capita × suicídio_total = –0,68  
  - inflacao × suicídio_total = –0,22 (quase nulo)  

---

## Conclusão

A análise exploratória realizada confirma que, no período estudado, **as crises econômicas brasileiras estiveram fortemente associadas ao aumento da taxa de suicídio**.  
- Enquanto a taxa global de suicídio diminuiu de forma quase contínua entre 2000–2021, o Brasil apresentou trajetória oposta após 2010, saltando de 4,7 para 7,0 por 100 mil habitantes.  
- O **desemprego** mostrou‐se o **principal preditor** de suicídio (correlação r ≈ +0,86), seguido pelo **PIB per capita** (r ≈ –0,68). Já a inflação revelou‐se pouco relevante para explicar variações na taxa de suicídio.  
- A **recessão de 2015–2016** elevou o desemprego para quase 13% em 2017, momento em que a taxa de suicídio ultrapassou 6,5 por 100 mil, mesmo com leve recuperação de PIB, evidenciando defasagem do mercado de trabalho.  
- O **choque pandêmico de 2020** aprofundou o cenário: PIB per capita caiu para US$ 7 100 e desemprego bateu 13,7%, gerando aumento adicional de suicídios que foi **maior do que o previsto apenas pelos indicadores econômicos**, revelando impactos sociopsicológicos extraeconômicos (isolamento, luto coletivo).  
- Em **2022–2023**, embora o PIB per capita tenha se recuperado (US$ 10 250) e o desemprego retornado a valores baixos (~7,9%), a taxa de suicídio permaneceu elevada (~6,3–6,4), indicando que os efeitos sobre a saúde mental persistem por anos após a crise.

**Pesquisa futura e limitações**  
- **Dados anuais** limitam a captação de variações sazonais (picos de inverno, datas comemorativas). Dados mensais ou trimestrais seriam ideais para modelagem mais precisa.  
- Incluir variáveis adicionais em modelos múltiplos (índice de violência, uso de álcool/drogas, acesso a CAPS, nível de escolaridade) para identificar determinantes sociais e comportamentais.  
- Análises de machine learning (random forest, XGBoost) e clusterização para mapear municípios de alto risco e recomendar intervenções localizadas.

---

## Referências

- **WHO API Athena**: https://ghoapi.azureedge.net/api/MH_12  
- **World Bank Indicators**: https://api.worldbank.org/  
- **IBGE. Taxa de Desemprego**: https://www.ibge.gov.br/