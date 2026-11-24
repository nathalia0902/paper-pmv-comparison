# Comparação entre os modelos PMV e PMV com efeito de resfriamento (PMVCE)

Este repositório contém o código, os dados e os resultados utilizados na análise comparativa dos modelos de conforto térmico PMV, conforme a ISO 7730:2005, e PMV com Cooling Effect (PMVCE), conforme a ASHRAE 55:2023.

O trabalho tem como objetivo avaliar a capacidade desses modelos de estimar a sensação térmica dos ocupantes em ambientes reais, utilizando dados da **ASHRAE Global Thermal Comfort Database II**.

## Referência do artigo

TARTARINI, Federico; SCHIAVON, Stefano. *Comparative analysis of PMV Models accuracy implemented in the ISO 7730:2005 and ASHRAE 55:2023*. Building and Environment, v. 275, 2025, artigo 112766.

DOI: https://doi.org/10.1016/j.buildenv.2025.112766

**Repositório original dos autores:**
https://github.com/FedericoTartarini/paper-pmv-comparison

Este trabalho parte do código disponibilizado pelos autores. As alterações locais realizadas para execução, análise e geração de resultados devem ser consideradas em conjunto com a implementação original.

## Estrutura do projeto

```text
├── Data/
│   ├── db_measurements_v2.1.0.csv.gz
│   ├── db_analysis.pkl.gz
│   └── db_metadata.csv
├── Manuscript/
│   └── src/
│       ├── figures/
│       ├── tables/
│       └── sections/
├── main.py
├── Pipfile
├── Pipfile.lock
└── README.md
```

### Principais arquivos

- `db_measurements_v2.1.0.csv.gz`: base original de medições da ASHRAE Global Thermal Comfort Database II.
- `db_analysis.pkl.gz`: conjunto de dados processado utilizado nas análises.
- `db_metadata.csv`: metadados associados à base de dados.
- `main.py`: implementação dos modelos, processamento dos dados, análises e geração de gráficos.
- `Pipfile` e `Pipfile.lock`: definição das dependências e versões registradas do ambiente Python.

## Ambiente de execução

O projeto utiliza Python 3.10.

As dependências estão descritas no `Pipfile` e as versões resolvidas estão registradas no `Pipfile.lock`.

Para instalar as dependências com Pipenv, utilize:

```bash
pip install pipenv
pipenv install --ignore-pipfile
pipenv shell
```

Caso utilize um ambiente virtual Python convencional, instale as dependências conforme o `Pipfile` e utilize a versão de Python indicada pelo projeto.

**Observação sobre as dependências:** o artigo menciona `pythermalcomfort` 2.8.1 na metodologia, enquanto o arquivo `Pipfile.lock` registra uma versão diferente. Essa diferença deve ser considerada ao tentar reproduzir exatamente os resultados publicados.

## Execução das análises

O comando:

```bash
python main.py
```

não executa a sequência completa de análises. O bloco principal do arquivo apenas fecha as figuras abertas.

As análises podem ser executadas individualmente por meio das funções definidas em `main.py`.

Por exemplo, para carregar os dados processados e calcular as métricas F1:

```bash
python -c "import main; main.df = main.importing_filtering_processing(load_preprocessed=True); main.table_f1_scores()"
```

A função `importing_filtering_processing()` permite carregar os dados já processados ou realizar novamente o processamento da base original.

**Atenção:** o processamento pode atualizar arquivos locais, incluindo o conjunto de dados processado e arquivos auxiliares do manuscrito. Recomenda-se manter cópias de segurança antes de executá-lo.

## Análises realizadas

O estudo compara os resultados dos modelos PMV e PMVCE considerando diferentes condições de análise:

- Base completa;
- Velocidade do ar igual ou superior a 0,2 m/s;
- Registros com medições de velocidade do ar em três alturas;
- Subconjunto filtrado considerando os limites de PMV e sensação térmica observada.

Entre as análises implementadas estão:

- Distribuição das variáveis de entrada;
- Distribuição da sensação e preferência térmica;
- Acurácia das previsões;
- Métricas F1 micro, macro e weighted;
- Comparação entre as previsões dos modelos e a sensação térmica observada;
- Distribuição das discrepâncias entre os modelos e as respostas dos ocupantes;
- Análise das discrepâncias em função das variáveis ambientais e pessoais.

## Resultados e interpretação

Os resultados obtidos mostram diferenças entre os modelos, mas não indicam superioridade absoluta de um deles em todas as métricas.

Na análise realizada:

- O PMVCE apresentou F1 micro superior ao PMV nos quatro cenários avaliados.
- O PMV apresentou F1 macro superior nos quatro cenários.
- O F1 weighted apresentou resultados dependentes do cenário analisado.

Esses resultados demonstram a importância de considerar diferentes métricas e a distribuição das classes ao avaliar a capacidade preditiva dos modelos.

## Figuras e tabelas

Os gráficos gerados pelas funções de análise são armazenados em:

```text
Manuscript/src/figures/
```

As tabelas utilizadas no manuscrito podem ser encontradas em:

```text
Manuscript/src/tables/
```

Os arquivos gerados localmente podem ser diferentes dos arquivos originalmente disponibilizados pelos autores, devido às análises e correções realizadas durante a reprodução.

## Créditos

Código e estrutura original desenvolvidos por Federico Tartarini e Stefano Schiavon, disponibilizados no repositório original do artigo.

Os dados utilizados pertencem à ASHRAE Global Thermal Comfort Database II e devem ser utilizados respeitando as condições de acesso e citação estabelecidas por seus responsáveis.
