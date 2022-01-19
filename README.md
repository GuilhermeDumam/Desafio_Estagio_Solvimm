# Desafio_Estagio_Solvimm
Código usado para resolver os exercícios para vaga de estágio em dados da Solvimm.
O exercício compunha de 6 perguntas sobre dois datasets ('movies.csv' e 'customer_rating.csv') a serem respondidas pela EDA.

## O código foi todo realizado pelo google colaboratory:
https://colab.research.google.com/.
Ao entrar no google colab por uma conta @gmail, você terá uma tela parecida com a imagem abaixo.
![image](https://user-images.githubusercontent.com/72059691/133719861-df52b9d7-d9e0-4dc4-8fb8-ecc6a5dad7e2.png)

Nessa tela, já podemos começar a escrever o nosso código e fazer a importação dos datasets necessários pro exercício.
A forma como se faz o dataset é a seguinte:

Clicamos no símbolo de uma pasta no canto esquerdo da interface, conforme imagem abaixo:
![image](https://user-images.githubusercontent.com/72059691/133720728-a82ea3a9-5f41-46ee-9dda-8b3ac109cf6e.png)


Em seguida, clicamos no símbolo de uma folha A4 que se chama "Fazer upload para o armazenamento da sessão":
![image](https://user-images.githubusercontent.com/72059691/133720361-2d187908-eea2-4d37-9db3-83432094344c.png)

Feito o upload, os datasets ficarão na aba esquerda abaixo das pastas que vieram como exemplo:
![image](https://user-images.githubusercontent.com/72059691/133720505-29f8a0f8-8b97-493b-b0c0-f16758c9bb68.png)

Bem!
Feito os uploads, podemos já começar a trabalhar no código.

## Código

A primeira coisa que fazemos para rodar nosso código, é importar as bibliotecas que vamos utilizar no exercício.

### Bibliotecas
- Pandas

```
Import pandas as pd
```
![image](https://user-images.githubusercontent.com/72059691/133721254-8ba46688-67d9-4966-add0-02656a0ff9e5.png)

Para esse exercício, não houve a necessidade de importar nenhuma outra biblioteca.

### Leitura dos datasets

Agora vamos precisar que os datasets sejam lidos pelo nosso código  e fiquem armazenados na memória para podermos manipulá-los posteriormente. A chamada para lermos é a seguinte:

```
df_movies = pd.read_csv('/content/movies.csv', sep = ';', names =['Movie_Id', 'movie'])
```
**Aqui nós criamos um objeto do tipo dataframe (df) e ele recebeu a leitura do nosso dataset (movies.csv) colocando um separador de ponto e vírgula e duas colunas com os nomes de 'Movie_Id' e 'movie'.**

**Faremos o mesmo para o dataset de avaliações dos clientes**

```
df_customers_rating = pd.read_csv('/content/customers_rating.csv', sep =';')
```

Feito a leitura, podemos rodar alguns códigos para vermos como estão inseridos os dados dentro dos dataframes: assim como quantidade de linhas, colunas; se há valores nulos, repitidos, além de outras informações.

```
(dataframe).info()
(dataframe).duplicated()
(dataframe).head()
(dataframe).tail()
```

Após a verificação inicial. Visto que não há valores duplicados e nulos, podemos começar nossa análise.

Quantos filmes estão disponíveis no dataset?

![image](https://user-images.githubusercontent.com/72059691/133722897-03f1e78d-4c29-4e9f-8de7-862610bd20c0.png)

**Conseguimos essa informação um simples ```df_movies.tail(5)```. Ele nos mostra as cinco últimas linhas do dataframe. No caso do nosso dataset de 'movies', consta 4499 filmes.

Qual é o nome dos 5 filmes com melhor média de avaliação?

![image](https://user-images.githubusercontent.com/72059691/133723156-8e7f64b9-ac6c-4948-b6ae-60c9fb6588fc.png)

**Obtivemos isso com ```df_total.groupby(by='Nome_Filme')['Rating'].mean().sort_values(ascending=False).head(5)```. A função ```.groupby``` Ela colocou a coluna 'Nome_Filme' como referência. Númeramos pela média das avaliações em forma decrescente, imprimos os cinco primeiros valores.**

Quais os 5 anos com menos lançamentos de filmes?

![image](https://user-images.githubusercontent.com/72059691/133723557-0033b892-3767-41e2-a501-aa4f95ca0988.png)

**O código para essa imagem é: ```df_movies_filter.groupby(by='Ano')['Nome_Filme'].count().sort_values(ascending = True).head(5)```. Agrupamos pela coluna Ano que criamos, e mostramos a quantidade ```.count()``` em ordem crescente, os cinco primeiros valores.**

Quantos filmes que possuem avaliação maior ou igual a 4.7, considerando apenas os filmes avaliados na última data de avaliação do dataset?

![image](https://user-images.githubusercontent.com/72059691/133723886-f91d77eb-ccf5-4b41-9447-ec5a4abe9e89.png)


**```media_avaliacao[media_avaliacao['Rating'] >= 4.7]['Nome_Filme'].count()```. Para chegarmos nesse código; nós precisamos primeiro transformar a coluna 'DATE' do dataset para um tipo que pudessemos manusar como data. ```df_total['Date']= pd.to_datetime(df_total['Date'])```. Após isso, colocamos dentro de uma nova variável os dados da última data disponível no dataset ```df_total[df_total['Date'] == df_total['Date'].unique().max()]```. **

Dos filmes encontrados na questão anterior, quais são os 10 filmes com as piores notas e
quais as notas?

![image](https://user-images.githubusercontent.com/72059691/133729676-551d5bf1-9c48-4256-9439-0a15d1a868fe.png)


**Para encontrarmos essa resposta é bem simples: ```avaliacao_ultima_data.groupby(by='Nome_Filme')['Rating'].mean().sort_values(ascending = True).head(10)```. Rodamos o dataframe que colocara 'Nome_Filme' como referência, e nos apresentará as 10 primeiras linhas com as médias de avaliações em ordem crescente. Com isso, teremos as menores notas do período de última data do dataset.**

Quais os id's dos 5 customer que mais avaliaram filmes e quantas avaliações cada um fez?

![image](https://user-images.githubusercontent.com/72059691/133729822-c588f0b7-50da-4ff1-b23c-a7ee0379568e.png)


**Pegamos da mesma lógica da pergunta anterior, só que agora colocaremos como referência, os IDs dos clientes 'Cust_Id'; e pegaremos desses clientes, quais fizeram mais avaliações e quantas foram. ```df_total.groupby(by='Cust_Id')['Rating'].count().sort_values(ascending=False).head(5)```**



















