# Git-Artigo

# 📖 Introdução

O ponto de partida para este projeto foi o interesse na Análise de Homicídios da População Negra no Brasil, um tema de profunda relevância social e estatística. O objetivo inicial era buscar dados que pudessem explicar as disparidades regionais na violência letal direcionada a esta parcela da população.

A partir dessa escolha, iniciamos a busca por bases de dados robustas e confiáveis:

Violência: Fomos atrás de bases de dados secundárias, como repositórios públicos e plataformas como o Kaggle, que frequentemente agregam dados de segurança pública e direitos humanos. Foi neste contexto que obtivemos a base de dados de homicídios por Unidade da Federação (UF) e etnia.

Fatores Socioeconômicos: Para cruzar as informações de violência com o contexto econômico, recorremos a fontes oficiais, como o Instituto Brasileiro de Geografia e Estatística (IBGE). Os dados de Produto Interno Bruto (PIB) e População (Censo 2022) foram cruciais para calcular o indicador de riqueza per capita.

A integração dessas bases permitiu que o projeto evoluísse para uma análise de correlação e regressão, investigando como a riqueza por habitante (PIB per capita) se relaciona com a Taxa de Homicídios da População Negra em cada estado brasileiro.


# 🛠️ Metodologia e Passos Chave do Código
O projeto seguiu rigorosamente os seguintes passos no código, utilizando principalmente as bibliotecas pandas (para manipulação de dados) e statsmodels (para análise estatística):

📝 Resumo Final do Projeto: Análise da Violência e PIB no Brasil
Este projeto de análise de dados investigou a relação entre o desenvolvimento econômico (medido pelo PIB per capita) e a violência letal (medida pela Taxa de Homicídios da População Negra) nos estados brasileiros.

1. 📖 Introdução e Desafio Metodológico
O tema central do estudo foi a Análise de Homicídios da População Negra. O principal desafio metodológico foi a incompletude dos dados em uma única fonte.

Necessidade de Fusão: Foi preciso juntar (merge) dados de múltiplas bases (informações de segurança pública de bases secundárias como Kaggle e dados de população e PIB do IBGE) para criar um dataset consolidado.

O Objetivo: O cruzamento desses dados permitiu calcular os indicadores de interesse e realizar a análise estatística.

2. 🛠️ Metodologia e Passos Chave do Código
O projeto seguiu rigorosamente os seguintes passos no código, utilizando principalmente as bibliotecas pandas (para manipulação de dados) e statsmodels (para análise estatística):

A. Preparação e Carregamento dos Dados
Criação Manual de Dados do IBGE:

Dados de Censo (pop_total, pop_negra) e PIB (pib_mil_reais) foram inseridos e salvos em CSV.
Código: Criação de dicionários e uso de pd.DataFrame() seguido de df.to_csv().

Carregamento e Filtragem:
Os dados de Homicídios (assumidamente carregados como df_homicidios_negros) foram filtrados pelo ano mais recente (2022/2023).
Código: df_2022 = df_homicidios_negros[df_homicidios_negros["período"] == 2022]


📝 Resumo Final do Projeto: Análise da Violência e PIB no Brasil
Este projeto de análise de dados investigou a relação entre o desenvolvimento econômico (medido pelo PIB per capita) e a violência letal (medida pela Taxa de Homicídios da População Negra) nos estados brasileiros.

1. 📖 Introdução e Desafio Metodológico
O tema central do estudo foi a Análise de Homicídios da População Negra. O principal desafio metodológico foi a incompletude dos dados em uma única fonte.

Necessidade de Fusão: Foi preciso juntar (merge) dados de múltiplas bases (informações de segurança pública de bases secundárias como Kaggle e dados de população e PIB do IBGE) para criar um dataset consolidado.

O Objetivo: O cruzamento desses dados permitiu calcular os indicadores de interesse e realizar a análise estatística.

2. 🛠️ Metodologia e Passos Chave do Código
O projeto seguiu rigorosamente os seguintes passos no código, utilizando principalmente as bibliotecas pandas (para manipulação de dados) e statsmodels (para análise estatística):

A. Preparação e Carregamento dos Dados
Criação Manual de Dados do IBGE:

Dados de Censo (pop_total, pop_negra) e PIB (pib_mil_reais) foram inseridos e salvos em CSV.

Código: Criação de dicionários e uso de pd.DataFrame() seguido de df.to_csv().

Carregamento e Filtragem:

Os dados de Homicídios (assumidamente carregados como df_homicidios_negros) foram filtrados pelo ano mais recente (2022/2023).

Código: df_2022 = df_homicidios_negros[df_homicidios_negros["período"] == 2022]

# B. Limpeza e Fusão (Merge)
Padronização da Chave de Merge:

Para garantir que o merge fosse bem-sucedido, a coluna de identificação dos estados (uf ou nome) foi padronizada em todas as bases.

Código: Foi utilizada a biblioteca unidecode para remover acentos antes de unificar os nomes: df['uf'] = df['uf'].apply(lambda x: unidecode.unidecode(x).upper()).

Fusão: Os DataFrames foram unidos sucessivamente (pd.merge), garantindo que, para cada estado, houvesse informações de homicídios, população e PIB.


# C. Cálculo das Variáveis Finais (Transformação de Dados)

Após a fusão bem-sucedida das bases de dados (Homicídios, Censo e PIB), o passo seguinte no código foi a transformação dos dados brutos em indicadores prontos para a análise estatística. As duas variáveis cruciais para a Regressão Linear foram calculadas neste momento: a Variável Preditiva (X) e a Variável Resposta (Y).


# D. Análise Estatística e Visualização

Correlação: Calculada a correlação de Pearson (scipy.stats.pearsonr) entre o pib_per_capita e a taxa_homicidios_negros.
Regressão Linear (OLS): Foi utilizado o método OLS (Mínimos Quadrados Ordinários) da biblioteca statsmodels.formula.api para testar a significância da relação.

# Top 10 Estados - Taxa de Homicídios de Negros (por 100 mil)
<img width="618" height="368" alt="image" src="https://github.com/user-attachments/assets/b910a054-7544-4be8-9c8a-9a43bb5b7231" />

# Top 10 estados com maior PIB per capita (2022)
<img width="741" height="369" alt="image" src="https://github.com/user-attachments/assets/6f92cb9e-9a71-49ec-8eec-33c889ff0d3b" />

# 💡 Resultados e Conclusão
Correlação Negativa: A análise estatística confirmou uma correlação negativa entre o PIB per capita e a Taxa de Homicídios da População Negra (r ≈ -0.56).

Significância: O modelo de Regressão Linear (OLS) indicou que essa relação é estatisticamente significativa.

Conclusão: Os resultados sugerem que, em média, estados com maior riqueza por habitante tendem a apresentar menores taxas de homicídio direcionado à população negra, indicando uma associação entre o desenvolvimento socioeconômico e a segurança pública.



# Comprovante
<img width="702" height="1600" alt="image" src="https://github.com/user-attachments/assets/750452fc-9516-4744-8547-884eaae4d07f" />





