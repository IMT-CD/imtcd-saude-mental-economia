# Projeto de Análise Exploratória de Dados (EDA)

## Sumário
- [Link para o Colab](#link-para-o-colab)
- [Vídeo do projeto](#vídeo-do-projeto)
- [Introdução](#introdução)  
- [Objetivo](#objetivo)  
- [Fontes de Dados](#fontes-de-dados)  
- [Metodologia](#metodologia)  
- [Desenvolvimento](#desenvolvimento)  
- [Conclusão](#conclusão)  
- [Perguntas e respostas](#perguntas-e-respostas)
- [Datafólio](#datafólio)
- [Referências](#referências)  

---

## Integrantes

- Nome: Erick Eiji Nagao - Ra: 21.00690-3  
- Nome: Igor Improta Martinez da Silva - Ra: 21.00834-5  
- Nome: Gabriel Henrique Baca Rado - Ra: 21.01286-5  
- Nome: Ryuske Hideaki Sato - Ra: 21.00745-4  
- Nome: Vinicius de Oliveira Berti - Ra: 21.01219-9  

---

## Link para o Colab

Para visualizar e executar o notebook diretamente no Google Colab, acesse:  
[saúde_mental_economia.ipynb no Colab](https://colab.research.google.com/github/ViniciusBerti/20241_maua_ecm252_intro_git/blob/main/saude_mental_economia.ipynb)

---

## Vídeo do Projeto

Assista à apresentação completa no YouTube:  
[https://youtu.be/3aCso8jSszo](https://youtu.be/3aCso8jSszo)

---

## Introdução

Crises econômicas têm impactos que vão muito além de indicadores como PIB ou inflação. Elas afetam diretamente a vida das pessoas, e esse reflexo também aparece na saúde mental da população. O suicídio, infelizmente, é um dos indicadores mais extremos desse sofrimento.

Segundo dados da Organização Mundial da Saúde (WHO), a média global de suicídios em 2021 foi de aproximadamente 9,0 por 100 mil habitantes. No Brasil, essa taxa foi ligeiramente inferior (∼7,5 por 100 mil), mas o crescimento entre 2019 e 2020 foi alarmante: aumento de 13%.

Durante o mesmo período, o país enfrentou crises econômicas marcantes, como a de 2015 e os efeitos da pandemia em 2020. A taxa de desemprego chegou a 13,9% em 2020 (IBGE), e o PIB per capita caiu significativamente.

Por que escolhemos este tema? Porque acreditamos que políticas econômicas devem considerar também seus efeitos sobre a saúde mental da população. Com o acesso a dados públicos via APIs da WHO e do World Bank, buscamos explorar essas relações de forma quantitativa, destacando padrões, tendências e desigualdades que merecem atenção.

---

## Objetivo

Investigar a relação entre variáveis econômicas — como desemprego e PIB per capita — e a taxa de suicídio no Brasil entre 2013 e 2021 (último ano com dados disponíveis). Através de uma análise exploratória rigorosa e visualmente clara, buscamos evidenciar os efeitos sociais das crises econômicas sobre a saúde mental da população. Além disso, temos como objetivo responder às seguintes seis perguntas-chave:

1. **A inflação tem impacto direto na taxa de suicídio no Brasil?**  
2. **A taxa de suicídio no Brasil está aumentando com o passar dos anos?**  
3. **A taxa de suicídio no mundo segue uma tendência de crescimento?**  
4. **Há uma correlação entre o aumento do desemprego e os casos de suicídio?**  
5. **Variações no PIB influenciam os índices de suicídio?**  
6. **Os dados indicam que a taxa de suicídio tende a aumentar nos próximos anos?**

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

![grafico 1](assets/grafico-1.png)

### Evolução da taxa de suicídio no Brasil por sexo (2000–2021)
- Homens passaram de 7,7 para 10,7 por 100 mil, e mulheres de 1,9 para 3,6. A razão homem:mulher caiu de ~4:1 para ~3:1, indicando maior crescimento relativo para o público feminino.

![grafico 2](assets/grafico-2.png)

### Evolução da taxa de desemprego no Brasil (2013–2023)
- Desemprego caiu de 7,1% (2013) para 6,8% (2014), subiu a 12,8% (2017) pela recessão de 2015–2016, atingiu 13,7% em 2020 (pandemia) e recuou para 7,9% em 2023.

![grafico 3](assets/grafico-3.png)

### Desemprego × PIB per capita no Brasil (2013–2023)
- Apesar de PIB per capita recuperar‐se em 2017 (US$ 10 350), o desemprego permaneceu alto (~12,8%), evidenciando defasagem. Em 2020, PIB caiu para US$ 7 100 e desemprego saltou a 13,7%. De 2021 a 2023, PIB voltou a US$ 10 250 e desemprego caiu para 7,9%.

![grafico 4](assets/grafico-4.png)

### Relação entre PIB per capita e Desemprego (2013–2023)
- Correlação negativa forte (r ≈ –0,85): anos como 2017 e 2020 destacam‐se por defasagens e choques simultâneos. Em 2020, o ponto “PIB baixo, desemprego alto” foi extremo.

![grafico 5](assets/grafico-5.png)

### Evolução da taxa de suicídio mundial (2013–2023)
- A taxa mundial caiu de ~10,12 para 8,89 entre 2013 e 2020, com leve alta a 8,90 em 2021. O Brasil seguiu trajetória oposta, reforçando que fatores internos pesaram mais que as tendências globais.

![grafico 6](assets/grafico-6.png)

### Taxa de suicídio no Brasil por sexo (2013–2023)
- Homens: 8,9 → 10,6; mulheres: 2,6 → 3,6. A razão caiu de ~3,4:1 para ~3:1. Mesmo após 2021, a taxa feminina continuou em alta, refletindo sobrecarga e vulnerabilidades específicas.

![grafico 7](assets/grafico-7.png)

### Taxa de desemprego no Brasil (2013–2023)
- Reforça o pico de 13,7% em 2020 e a rápida recuperação a 7,9% em 2023, em contraste com a defasagem pós‐2015, quando o desemprego permaneceu alto mesmo com leve recuperação de PIB.

![grafico 8](assets/grafico-8.png)

### Desemprego × PIB per capita no Brasil (2013–2023)
- Confirma correlação inversa (r ≈ –0,82). Em 2017, PIB subiu a US$ 10 350 e desemprego manteve‐se alto, mostrando defasagem. Em 2020, choques simultâneos de PIB e desemprego reforçam correlação quase instantânea.

![grafico 9](assets/grafico-9.png)

### Correlação – Desemprego vs. Taxa de suicídio (2013–2023)
- Correlação positiva forte (r ≈ +0,86). Em 2017 e 2021, a taxa de suicídio ficou acima do valor previsto pelo desemprego, indicando efeitos adicionais (recessão prolongada, pandemia).

![grafico 10](assets/grafico-10.png)

### Correlação – PIB per capita vs. Taxa de suicídio (2013–2023)
- Correlação negativa moderada (r ≈ –0,68). Em 2017 e 2020–2021, a taxa de suicídio superou o valor previsto apenas pelo PIB, destacando impactos sociopsicológicos extraeconômicos.

![grafico 11](assets/grafico-11.png)

### Matriz de correlação (2013–2023)
- Principais correlações:  
  - desemprego × suicídio_total = +0,86  
  - pib_per_capita × suicídio_total = –0,68  
  - inflacao × suicídio_total = –0,22 (quase nulo)

![grafico 12](assets/grafico-12.png)

### Modelagem de Séries Temporais: previsão da taxa de suicídio (2000–2026)

Para projetar a evolução futura da taxa de suicídio no Brasil, ajustamos um modelo ARIMA à série anual de 2000 a 2022 e geramos previsões até 2026:

1. **Preparação e estacionariedade**  
   - A série original (2000–2022) não era estacionária.  
   - Foram necessárias três diferenciações (d = 3) para obter uma série estacionária (estatística ADF ≈ –3,99, p-valor ≈ 0,0014).

2. **Seleção de parâmetros (p, d, q)**  
   - Com base nos gráficos de ACF e PACF da série diferenciada, adotamos um ARIMA(1, 3, 1).

3. **Ajuste do modelo**  
   - Parâmetros estimados:  
     - ar.L1 ≈ –0,46 (insignificante ao nível de 5%)  
     - ma.L1 ≈ –0,99 (insignificante ao nível de 5%)  
     - σ² ≈ 0,0856  
   - Diagnóstico de resíduos:  
     - Ljung–Box p ≈ 0,89 → sem autocorrelação remanescente.  
     - Jarque–Bera p ≈ 0,50 → resíduos próximos de normalidade.  
     - Teste de heteroscedasticidade p ≈ 0,38 → sem indícios fortes de variância não constante.

4. **Previsões (2023–2026)**  
   - A partir de 2022 (6,95 por 100 mil), o modelo ARIMA indica:  
     - **2023**: 9,10  
     - **2024**: 9,70  
     - **2025**: 10,05  
     - **2026**: 10,40  
   - O gráfico resultante mostra a série histórica em azul até 2022 e os pontos vermelhos previstos de 2023 a 2026, indicando que a tendência de alta na taxa de suicídio deve prosseguir nos próximos anos, embora com ritmo de crescimento mais ameno.

![grafico 13](assets/output.png)

### Teste de Correlação de Pearson (Desemprego × Suicídio)

Aplicamos `pearsonr` para medir a associação entre desemprego (%) e taxa de suicídio (por 100 mil habitantes) no Brasil (2013–2023). Após alinhar as séries e remover valores ausentes, obtivemos:

- **Correlação de Pearson:** r ≈ 0,86  
- **p-valor:** p < 0,001  

**Interpretação prática:**  
Essa correlação positiva forte significa que, no período analisado, sempre que a taxa de desemprego subiu, a taxa de suicídio também aumentou. Em termos concretos, anos com desemprego acima de 12% (2016–2017, 2020) coincidiram com picos na taxa de suicídio. Assim, medidas que influenciam o desemprego tendem a ter impacto direto na saúde mental da população, elevando o risco de suicídio em períodos de crise.

### Teste de Hipótese para a Correlação de Pearson (Visualização)

Para confirmar estatisticamente a associação entre desemprego e taxa de suicídio, realizamos o teste t para correlação de Pearson. O gráfico abaixo ilustra a distribuição t sob H₀ e o valor t observado, t_obs ≈ 4,43 (n = 11 anos, graus de liberdade = 9):

- **H₀:** ρ (correlação populacional) = 0  
- **t_obs:** 4,43  
- **df:** 9  
- **Região crítica (α = 0,05, bicaudal):** |t| > 2,262  

Como t_obs = 4,43 está muito à direita da curva (fora da região de não-rejeição), rejeitamos H₀. A correlação r ≈ 0,86 é estatisticamente significativa (p < 0,001).

**Interpretação prática:**  
O valor t_obs = 4,43 e a região crítica triangular pintada em vermelho confirmam que a correlação não é fruto do acaso. Na prática, isso significa que políticas que afetem o nível de desemprego terão efeitos mensuráveis sobre a taxa de suicídio — um dado que não pode ser ignorado em decisões de governo. O gráfico deixa claro que o padrão de associação observado não é aleatório, mas sim reflexo de uma relação real e robusta.

![grafico 14](assets/grafico-14-pearson.png)

### Teste t de Diferença entre Taxas de Suicídio de Homens e Mulheres

Para verificar se as médias de suicídio de homens e de mulheres diferem significativamente (2013–2023), usamos o teste t de Student (Welch):

1. **H₀:** μ_homens = μ_mulheres  
2. **t_obs:** ≈ 34,26  
3. **Graus de liberdade (Welch):** ≈ 17  
4. **Região crítica (α = 0,05, bicaudal):** |t| > 2,110  

Como t_obs = 34,26 está muito acima de 2,110, rejeitamos H₀.

**Interpretação prática:**  
Essa diferença altíssima entre as médias (homens ~10,6 por 100 mil vs. mulheres ~3,6 por 100 mil) mostra que o risco de suicídio para homens é estatisticamente e expressivamente maior do que para mulheres. Na prática, significa que qualquer programa de prevenção deve priorizar estratégias específicas para cada gênero, pois fatores culturais, sociais e psicológicos impactam muito mais o público masculino.

![grafico 15](assets/grafico-15-ttest.png)

---

## Conclusão

A análise exploratória realizada confirma que, no período estudado, **as crises econômicas brasileiras estiveram fortemente associadas ao aumento da taxa de suicídio**.  
- Enquanto a taxa global de suicídio diminuiu de forma quase contínua entre 2000–2021, o Brasil apresentou trajetória oposta após 2010, saltando de 4,7 para 7,0 por 100 mil habitantes.  
- O **desemprego** mostrou‐se o **principal preditor** de suicídio (correlação r ≈ +0,86, p < 0,001), seguido pelo **PIB per capita** (r ≈ –0,68, p < 0,01). Já a inflação revelou‐se pouco relevante para explicar variações na taxa de suicídio (r ≈ –0,22).  
  - O teste t confirmatório mostrou t_obs ≈ 4,43 (df = 9), bem acima do limite crítico (±2,262), reforçando que essa correlação não se deve ao acaso, mas reflete uma relação estatisticamente significativa entre desemprego e suicídio.  
- A **recessão de 2015–2016** elevou o desemprego para quase 13% em 2017, momento em que a taxa de suicídio ultrapassou 6,5 por 100 mil, mesmo com leve recuperação de PIB, evidenciando defasagem do mercado de trabalho e efeito tardio na saúde mental.  
- O **choque pandêmico de 2020** aprofundou o cenário: PIB per capita caiu para US$ 7 100 e desemprego bateu 13,7%, gerando aumento adicional de suicídios que foi **maior do que o previsto apenas pelos indicadores econômicos**—um sinal de impactos sociopsicológicos extraeconômicos (isolamento, luto coletivo).  
- Em **2022–2023**, embora o PIB per capita tenha se recuperado (US$ 10 250) e o desemprego retornado a valores baixos (~7,9%), a taxa de suicídio permaneceu elevada (~6,3–6,4), indicando que os efeitos sobre a saúde mental persistem por anos após a crise.  
- Comparando gêneros, comprovamos por meio de teste t (t_obs ≈ 34,26, df ≈ 17, valor crítico ±2,110) que a diferença entre a média anual de suicídio dos **homens (~10,6 por 100 mil)** e das **mulheres (~3,6 por 100 mil)** é estatisticamente significativa (p < 0,001). Na prática, isso reforça a necessidade de políticas de prevenção específicas para cada gênero, visto que o risco masculino é muito superior.  
- Finalmente, a modelagem ARIMA(1,3,1) projetou **7,34 suicídios por 100 mil em 2022** e **7,83 em 2023**, sugerindo que, sem intervenções estruturais, a taxa continuará em trajetória de alta, embora em ritmo levemente mais lento comparado a 2020–2021.

**Pesquisa futura e limitações**  
- **Dados anuais** limitam a captação de variações sazonais (picos de inverno, datas comemorativas). Dados mensais ou trimestrais seriam ideais para modelagem mais precisa.  
- Incluir variáveis adicionais em modelos múltiplos (índice de violência, uso de álcool/drogas, acesso a CAPS, nível de escolaridade) para identificar determinantes sociais e comportamentais.  
- Análises de machine learning (random forest, XGBoost) e clusterização para mapear municípios de alto risco e recomendar intervenções localizadas.

---

## Perguntas e respostas

1. **A inflação tem impacto direto na taxa de suicídio no Brasil?**  
   Não. A análise mostrou uma correlação negativa muito fraca entre inflação e taxa de suicídio, indicando que a inflação não exerce um efeito significativo sobre os casos de suicídio no país.
   ![Questão 1 - Correlação entre inflação e taxa de suicídio](assets/grafico-12.png)

2. **A taxa de suicídio no Brasil está aumentando com o passar dos anos?**  
   Sim. Há uma tendência clara de crescimento da taxa de suicídio no Brasil ao longo de todos os anos analisados. Esse aumento é consistente e persistente, não se limitando a flutuações pontuais.
   ![Questão 2 - Taxa de suicídio no Brasil evolução](assets/grafico-2.png)

3. **A taxa de suicídio no mundo segue uma tendência de crescimento?**  
   Não. Ao contrário do Brasil, a taxa global de suicídio vem caindo de forma contínua nos últimos anos, passando de aproximadamente 13,7 para 8,9 por 100 mil habitantes entre 2000 e 2021.
   ![Questão 3 - Taxa de suicídio mundial](assets/grafico-1.png)

4. **Há uma correlação entre o aumento do desemprego e os casos de suicídio?**  
   Sim. O desemprego apresentou uma correlação extremamente forte (r ≈ +0,86) com a taxa de suicídio, confirmada estatisticamente por testes de hipótese. Anos de desemprego elevado coincidem diretamente com picos de suicídio, especialmente em 2017 e 2020–2021.
   ![Questão 4 - Correlação entre desemprego e taxa de suicídio](assets/grafico-10.png)

5. **Variações no PIB influenciam os índices de suicídio?**  
   Sim. O PIB per capita mostrou uma correlação negativa moderada (r ≈ –0,68) com a taxa de suicídio: quando o PIB cai, a incidência de suicídios tende a aumentar. Em momentos de crise econômica (2017 e 2020), mesmo com leve recuperação do PIB, o suicídio permaneceu acima do esperado, indicando impactos socioemocionais profundos..
   ![Questão 5 - Correlação entre pib e taxa de suicídio](assets/grafico-11.png)

6. **Os dados indicam que a taxa de suicídio tende a aumentar nos próximos anos?**  
   Sim. A previsão com modelo ARIMA estimou que a taxa de suicídio continuará em elevação, partindo de 6,95 por 100 mil habitantes em 2022 para:  
  - **2023:** 9,10 por 100 mil hab.  
  - **2024:** 9,70 por 100 mil hab.  
  - **2025:** 10,05 por 100 mil hab.  
  - **2026:** 10,40 por 100 mil hab.  

  Esse cenário só será revertido se ocorrerem melhorias econômicas consistentes e intervenções eficazes de saúde mental.
   ![Questão 6 - Previsão da taxa de suicídio no Brasil](assets/output.png)

---

## Datafólio

![datafolio](datafolio-png.png)

---

## Referências

- **WHO API Athena**: https://ghoapi.azureedge.net/api/MH_12  
- **World Bank Indicators**: https://api.worldbank.org/  
- **IBGE. Taxa de Desemprego**: https://www.ibge.gov.br/
