# Sinistros de Trânsito na Cidade de Fortaleza (2015-2024)

Análise exploratória e testes estatísticos sobre **130.820 sinistros de trânsito** registrados em Fortaleza entre 2015 e 2024. O objetivo é entender **quando, onde e com quais veículos** os sinistros acontecem e o que está associado às **mortes** (variável alvo), para apoiar decisões de segurança viária.

> Projeto acadêmico desenvolvido no **Instituto Federal do Ceará (IFCE)**, sob orientação do **Prof. Dr. Valberto Feitosa**.

## Equipe

- Anady Carvalho
- João Pedro Martins
- Jordan Elias Barbosa
- Jordan Elizeu Barbosa
- Márcio Rosário

## Conteúdo do repositório

| Arquivo | Descrição |
|---|---|
| `eda.ipynb` | Análise exploratória em 11 passos, com testes de hipóteses |
| `vias_acidentes_2.ipynb` | Ranking das 18 vias com mais sinistros, estatísticas e mapa |
| `sinistro_transito_final.csv` | Base final tratada (130.820 linhas e 27 colunas) |
| `Sinistros_Transito_Fortaleza_2015_2024_v5.pptx` | Apresentação executiva do projeto |

## Sobre a base de dados

- **Linhas:** 130.820 sinistros (período de 2015 a 2024)
- **Colunas:** 27
- **Variável alvo:** `mortos` (número de mortes por sinistro)
- **Principais colunas:** `data`, `horaint`, `faixahoraria`, `fimdesemana`, `bairro`, `rua`, `latitude`, `longitude`, `tipocruzamento`, `controletrafego`, `usosolo`, `natureza`, `severidade`, `mortos`, `feridos`, `ilesos`, colunas de veículos (`automovel`, `motocicleta`, `onibus`, `bicicleta`, `caminhao`, `microonibus`, `ciclomotor`, `tracaoanimal`, `trem`) e `totalveiculos`

A base já está tratada: textos padronizados e colunas derivadas, como hora inteira, faixa horária, fim de semana e total de veículos.

## Roteiro da análise (`eda.ipynb`)

| Passo | Tema |
|---|---|
| 1 | Análise descritiva e evolução anual |
| 2 | Horários em que mais ocorrem os sinistros |
| 3 | Faixa de horário e fim de semana |
| 4 | Bairros com mais sinistros e mais mortes |
| 5 | Veículos envolvidos |
| 6 | Co-ocorrência de veículos no mesmo sinistro |
| 7 | Variáveis que mais influenciam as mortes |
| 8 | Correlação entre variáveis numéricas |
| 9 | Qui-quadrado entre variáveis categóricas |
| 10 | Relação entre variáveis numéricas e categóricas (R²) |
| 11 | Cinco testes de hipóteses |

## Principais resultados

- **Gravidade:** 72,3% dos sinistros deixam feridos (94.597) e 1,47% são fatais (1.926). Foram 1.986 mortes no período.
- **Evolução:** 2015 a 2017 tiveram mais de 16 mil sinistros por ano; o mínimo foi 2020 (9.230).
- **Horários:** picos às 16h (8.172) e às 7h (8.066). A tarde concentra mais sinistros (45.401), mas **madrugada (2,22%) e noite (2,13%)** têm a maior taxa de mortes por sinistro.
- **Dias:** 72,7% dos sinistros ocorrem em dias úteis e 27,3% em fins de semana.
- **Bairros:** o Centro lidera em sinistros (7.464) e em mortes (73).
- **Veículos:** automóveis (51,8%) e motocicletas (40,0%) somam mais de 91% dos veículos envolvidos. As maiores taxas de mortes por sinistro aparecem com ciclomotores (5,21%), caminhões (3,89%) e ônibus (3,64%).
- **Vias críticas:** a Rodovia CE-040 concentra 2.035 dos 9.872 sinistros das 18 vias analisadas (20,6%), e as 5 primeiras vias somam 47,8%.

### Hipóteses testadas

| Hipótese | Teste | Decisão |
|---|---|---|
| H1: mortes são mais frequentes na madrugada e/ou fim de semana | Qui-quadrado (χ² = 107,98; V de Cramér = 0,029) | Rejeita H0: há relação (efeito fraco) |
| H2: motos aumentam o número de feridos | ANOVA e Pearson (r = 0,304) | Rejeita H0: há relação |
| H3: o número mensal de sinistros tem tendência de queda | Regressão linear (R² = 0,416) | Rejeita H0: há relação com o tempo |
| H4: a gravidade depende do controle de tráfego | Qui-quadrado (χ² = 22.954,92; V de Cramér = 0,242) | Rejeita H0: há relação |
| H5: sinistros por bairro são explicados por motos e cruzamentos | Regressão múltipla (R² = 0,951) | Rejeita H0: há relação |

## Como executar

1. Clone o repositório e mantenha os arquivos na mesma pasta (os notebooks leem `sinistro_transito_final.csv`).
2. Instale as dependências:

   ```bash
   pip install pandas numpy matplotlib seaborn scipy statsmodels jupyter
   ```

3. Abra os notebooks:

   ```bash
   jupyter notebook
   ```

## Tecnologias

Python, pandas, NumPy, Matplotlib, Seaborn, SciPy e statsmodels.

## Limitações e cuidados

- Com mais de 130 mil registros, até diferenças pequenas ficam estatisticamente significativas. Observe o **tamanho do efeito** (por exemplo, V de Cramér = 0,029 na H1, que é fraco).
- Os testes mostram **associação**, não causa.
- Na H5, bairros maiores têm mais motos e mais sinistros, então o R² alto deve ser lido com cautela.
- No `vias_acidentes_2.ipynb`, o texto do relatório cita média de 493,6 e mediana de 390 sinistros por via, valores da tabela antes de unir vias repetidas. Depois da unificação (18 vias), os valores são 548,4 e 427.
- As posições das vias no mapa do `vias_acidentes_2.ipynb` são aproximadas e servem apenas para ilustração.
- Parte das colunas tem informação ausente, como `controletrafego`, que aparece como "não informado" em 61% dos registros.
