# Tratamento de dados em Python e criação de Dashboard utilizando PowerBI

O objetivo é tratar um conjunto de dados selecionado aleatoriamente (sem conhecimento prévio) e realizar o processo de tratamento de dados e criação de um Dashboard utilizando PowerBI

## Informações relevantes

- #### Origem do Dataset: https://www.kaggle.com/datasets/aungpyaeap/supermarket-sales

- #### Abaixo, uma tabela contendo o significado de termos utilizados com frequência

| Termo | Significado |
|---|---|
| Count | Contagem de observações (frequência) de um determinado valor ou conjunto de valores. |
| Mean | Média aritmética: soma de todos os valores dividida pelo número total de valores. Representa o valor central de um conjunto de dados. |
| Std | Desvio padrão: medida da dispersão dos dados em relação à média. Indica o quanto os valores individuais se afastam da média. |
| Min | Valor mínimo: menor valor presente no conjunto de dados. |
| 25% | Primeiro quartil (Q1): valor abaixo do qual 25% dos dados se encontram. |
| 50% | Segundo quartil (Q2) ou mediana: valor que divide o conjunto de dados em duas partes iguais. |
| 75% | Terceiro quartil (Q3): valor abaixo do qual 75% dos dados se encontram. |
| Max | Valor máximo: maior valor presente no conjunto de dados. |
| Dataset | Refere-se a um conjunto de dados. |

## Renomeação das colunas do dataset

O dataset original continha as colunas nomeadas em inglês, para facilitar a visualização, segue a tradução e descrição de todas as colunas:

| Nome Original             | Nome Atual                | Descrição                                       |
|---------------------------|---------------------------|-------------------------------------------------|
| `InvoiceId`               | `IdFatura`                | Identificador único da fatura da venda           |
| `Branch`                  | `Filial`                  | Código da filial onde a venda foi realizada      |
| `City`                    | `Cidade`                  | Nome da cidade onde a venda ocorreu             |
| `CustomerType`            | `TipoCliente`             | Tipo de cliente (Membro ou Normal)              |
| `Gender`                  | `Gênero`                  | Gênero do cliente                               |
| `ProductLine`             | `LinhaProduto`            | Categoria de produto                            |
| `UnitPrice`               | `PrecoUnitario`           | Preço unitário do produto                       |
| `Quantity`                | `Quantidade`              | Quantidade de produtos comprados                |
| `Tax5Percent`             | `Imposto5Porcento`        | Valor do imposto de 5% sobre a venda            |
| `TotalAmount`             | `ValorTotal`              | Valor total da compra                           |
| `TransactionDate`         | `DataTransacao`           | Data em que a transação foi realizada           |
| `TransactionTime`         | `HoraTransacao`           | Hora da transação                               |
| `PaymentMethod`           | `MetodoPagamento`         | Método de pagamento usado (Ewallet, Cash, etc.) |
| `COGS`                    | `CustoMercadoriasVendidas`| Custo das mercadorias vendidas (CMV)            |
| `GrossMarginPercentage`   | `PercentualMargemBruta`   | Percentual da margem bruta                      |
| `GrossIncome`             | `RendaBruta`              | Lucro bruto da venda                            |
| `Rating`                  | `Avaliacao`               | Avaliação do cliente em relação à experiência   |

Codigo utilizado para renomear as colunas no dataset:

```python

#utilizamos uma função para renomar as colunas com base na ordem do dataset original, portanto, a ordem não foi alterada

dataset.columns = [
    'IdVenda', 'Filial', 'Cidade', 'TipoCliente', 'Gênero',
    'LinhaProduto', 'PrecoUnitario', 'Quantidade', 'Imposto5Porcento', 'ValorTotal',
    'DataTransacao', 'HoraTransacao', 'MetodoPagamento', 'CustoMercadoriasVendidas',
    'PercentualMargemBruta', 'RendaBruta', 'Avaliacao'
]

```

## Explorando o conjunto de dados

Funções utilizadas:

```python
dataset.head() # demonstra os dados nas posições iniciais (1)

dataset.tail() # demonstra os dados nas posições finais (2)

dataset.sample() # seleciona posições aleatórias e demonstra os dados (3)

```

Resultado (1):

![image](https://github.com/user-attachments/assets/ccac7ac1-6d1d-4182-bd26-0920b3a59672)

Resultado (2):

![image](https://github.com/user-attachments/assets/290fdb32-77a6-4ce1-bfa2-5679b6d42805)

Resultado (3):

![image](https://github.com/user-attachments/assets/cf672fd0-ee58-42c5-bfc4-2d4afcdbb1e4)

## Verificando se os dados estão seguindo todos os requisitos necessários

Os dados devem cumprir os seguintes requisitos:

- Duplicidade
- Consistência
- Completude
- Conformidade
- Integridade

Para que uma análise de dados possa ser feita corretamente, é necessário que o conjunto de dados esteja em sintonia perfeita com todos esses requisitos, dessa forma, podemos minimizar a chance de conclusões precipitadas e _insights_ incorretos. 

Verificando a existência de valores nulos:

```python
dataset.isnull().sum() # (4)
```

Resultado (4): 

![image](https://github.com/user-attachments/assets/c9f0a8f5-47fa-47e1-8160-4947573f5993)

#### Verificando os dados das colunas categoricas

Colunas categóricas existentes:

- Gênero
- Cidade
- Linha de produto
- Filial
- Método de pagamento
- Tipo de cliente

#### Criando gráficos para a visualização das colunas categóricas

```python

#as funções abaixo são responsáveis pela criação dos gráficos que facilitam a visualização do conjunto de dados

srn.barplot(dataset['Gênero']).set_title = 'Gênero' #(5)

srn.barplot(dataset['Cidade']).set_title = 'Cidade' #(6)

srn.barplot(dataset['LinhaProduto']).set_title = 'Setor de produtos' #(7)

srn.barplot(dataset['Filial']).set_title = 'Filial' #(8)

srn.barplot(dataset['MetodoPagamento']).set_title = 'Método de Pagamento' #(9)

srn.barplot(dataset['TipoCliente']).set_title = 'TipoCliente'#(10)

```

Resultado (5):

![image](https://github.com/user-attachments/assets/85858fe4-5390-4b52-b223-3012c720b1fc)

Resultado (6):

![image](https://github.com/user-attachments/assets/6543384c-d47b-4022-9318-f4cc255ba43d)

Resultado (7), note que as linhas não estão traduzidas:

![image](https://github.com/user-attachments/assets/b0cd8fca-987a-4e44-a156-3a529c24b2b8)

Resultado (8):

![image](https://github.com/user-attachments/assets/77b033e6-e23d-4a1d-bf6b-a566c62f8152)

Resultado (9):

![image](https://github.com/user-attachments/assets/925b15c1-d731-43f7-a11d-d0414699d591)

Resultado (10):

![image](https://github.com/user-attachments/assets/f6837fa1-1e56-4819-bdd3-be796f1076cc)

#### Criando agrupamentos

Sabendo que possuímos mil linhas, a soma da quantidade de dados de cada categoria deve ser igual a 1000, visto que cada linha pode conter apenas uma categória do número total de categórias, por exemplo, a coluna de cidades não pode conter duas cidades ao mesmo tempo.

```python

#Agrupando a coluna de gêneros:

agrupado1 = dataset.groupby(dataset['Gênero']).size() #(11)

#Agrupando a coluna de cidades:

agrupado2 = dataset.groupby(dataset['Cidade']).size() #(12)

#Agrupando a coluna de linha de produtos:

agrupado3 = dataset.groupby(dataset['LinhaProduto']).size() #(13)

#Agrupando a coluna de filiais:

agrupado4 = dataset.groupby(dataset['Filial']).size() #(14)

#Agrupando a coluna de métodos de pagamento

agrupado5 = dataset.groupby(dataset['MetodoPagamento']).size() #(15)

#Agrupando a coluna de tipos de clientes

agrupado6 = dataset.groupby(dataset['TipoCliente']).size() #(16)

```

#### Verificando os agrupamentos individualmente:

Resultado (11):

![image](https://github.com/user-attachments/assets/5220ac66-e576-46a4-b379-0aa99039a644)

Resultado (12):

![image](https://github.com/user-attachments/assets/5ba5b301-3dbf-4e17-a46b-e2cc13645cd9)

Resultado (13):

![image](https://github.com/user-attachments/assets/807c4461-59b6-43fc-ab69-0e764ffe09f7)

Resultado (14):

![image](https://github.com/user-attachments/assets/658f741e-a7ae-45fa-b02f-5834c14369c0)

Resultado (15):

![image](https://github.com/user-attachments/assets/8c4a3586-059b-42c7-b7c4-34963156778c)

Resultado (16):

![image](https://github.com/user-attachments/assets/65f590a6-c287-4cc8-9521-7667f983c0d8)

#### Conferindo os resultados e realizando as somas:
---

| Gênero        | Total |
|-----------------|-------|
| Feminino        | 501   |
| Masculino       | 499   |
| ***Gênero Total*** | ***1000*** |

---

| Cidade    | Total |
|-----------|-------|
| Mandalay  | 332   |
| Naypyitaw | 328   |
| Yangon    | 340   |
| **Total**  | 1000   |

---

| Produto             | Total |
|---------------------|-------|
| Eletrônicos         | 170   |
| Moda               | 178   |
| Alimentos           | 174   |
| Saúde               | 152   |
| Casa                | 160   |
| Esportes            | 166   |
| **Total**            | 1000   |

---

| Filial | Total |
|-------|-------|
| A     | 340   |
| B     | 332   |
| C     | 328   |
| **Total** | 1000   |

---

| Método de Pagamento | Total |
|---------------------|-------|
| Cash                | 344   |
| Credit card         | 311   |
| Ewallet              | 345   |
| **Total**            | 1000   |

---

| Tipo de Cliente | Total |
|----------------|-------|
| Member          | 501   |
| Normal          | 499   |
| **Total**        | 1000   |

---

#### Verificando as colunas númericas:

Colunas númericas existentes:

- Id de venda
- Preço unitário
- Imposto de 5%
- Quantidade
- Custo de mercadorias vendidas
- Percentual de margem bruta
- Renda bruta
- Avaliação
- Data da transação
- Hora da transação

As colunas númericas também precisam estar em alinhamento com os requisitos para a realização da análise de dados, podemos utilizar o comando "**describe**" para resumirmos cada coluna e identificar possíveis problemas:

```python
dataset['IdVenda'].describe() #(17)

dataset['PrecoUnitario'].describe() #(18)

dataset['Imposto5Porcento'].describe() #(19)

dataset['Quantidade'].describe() #(20)

dataset['CustoMercadoriasVendidas'].describe() #(21)

dataset['PercentualMargemBruta'].describe() #(22)

dataset['RendaBruta'].describe() #(23)

dataset['Avaliacao'].describe() #(24)

dataset['DataTransacao'].describe() #(25)

dataset['HoraTransacao'].describe() #(26)

```

Resultado (17):

![image](https://github.com/user-attachments/assets/040e01c5-daa5-4313-840e-8ff3c28f8cdd)

Resultado (18):

![image](https://github.com/user-attachments/assets/01aba312-a88a-4118-8c7d-d8d5a3a7de17)

Resultado (19):

![image](https://github.com/user-attachments/assets/457b3beb-3c9c-47f9-a048-47a31f1aaaed)

Resultado (20):

![image](https://github.com/user-attachments/assets/a5d14c91-912f-4a6b-bce5-0e15b39f7a37)

Resultado (21):

![image](https://github.com/user-attachments/assets/b425cc10-1d1b-4932-ae03-ffc43590f546)

Resultado (22):

![image](https://github.com/user-attachments/assets/1c38b0a3-e3ca-48bd-9697-75b4980d118c)

Resultado (23):

![image](https://github.com/user-attachments/assets/49dd0c8a-1549-472a-a20a-0c2ae334e439)

Resultado (24):

![image](https://github.com/user-attachments/assets/2fb58a72-3f53-405a-9d48-6d9436ddb8e3)

Resultado (25):

![image](https://github.com/user-attachments/assets/2751014d-d445-4dfe-b5c1-dd0b86ebaa79)

Resultado (26):

![image](https://github.com/user-attachments/assets/9ea4a755-7e94-4c95-ac41-7e3325021277)
