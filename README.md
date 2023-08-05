![GitHub repo size](https://img.shields.io/github/repo-size/iuricode/README-template?style=for-the-badge)
![GitHub forks](https://img.shields.io/github/forks/iuricode/README-template?style=for-the-badge)

# Teste Engenheiro de Dados Sênior

> Projeto que utiliza de uma base de dados disponível na web para criar arquivos .parquet, delta live tables, mergear dados entre arquivos e responder questões pontuais.

### Tarefas

O projeto o prjeto foi desenvolvido no decorrer de um dia útil concluindo tarefas como:

- [x] Tarefa 1 - Conectar com base de dados Ecommerce type disponível em https://uibakery.io/sql-playground ;
- [x] Tarefa 2 - Desenhar diagrama ER do banco;
- [x] Tarefa 3 - Criar notebook no Databricks Community;
- [x] Tarefa 4 - Criar lógica no notebook para leitura de cada tabela da base de dados e salvar cada uma tabela como .parquet;
- [x] Tarefa 5 - Criar merge entre arquivos da base de dados e arquivos .parquet contendo lógica de insert, update e delete para o mesmo, atualizando a delta table;
- [x] Tarefa 6 - Responder respectivas questões:
  Qual país possui a maior quantidade de itens cancelados?
  Qual o faturamento da linha de produto mais vendido, considerando como itens "Shipped", cujo o pedido foi realizado no ano de 2005?
  Informar nome, sobrenome e email dos vendedores do Japão com local-part do email mascarado.
- [x] Tarefa 7 - Salvar resultados em Delta Live Table;
- [x] Tarefa 8 - Armazenar artefatos em repositório Github público;
- [x] Tarefa 9 - Documentar no README.md todo o processo realizado.

## 💻 Pré-requisitos

Antes de começar, verifique se você atendeu aos seguintes requisitos:

* Você realizou o cadastro no Databricks Community no link (https://community.cloud.databricks.com).
* Você realizou conexão com a base de dados ecommerce type em (https://uibakery.io/sql-playground).

## 🚀 Iniciando Teste Engenheiro de Dados Sênior

# Módulos e frameworks:
  repositório: pyspark.sql
  módulos: SparkSession, DataFrame, functions

  repositório: delta.tables
  módulos: all

  repositório: pyspark.sql.utils
  módulos: AnalyssisException

# Conexão com base de dados:
Após informadas credenciais de acesso à base de dados Ecommece type, é criada uma sparksession utilizando as então credenciais.

# Declaração de funções úteis:
Declarada função "lerTabela" de leitura de tabela da base de dados JDBC pedindo que seja apenas informado nome da tabela para leitura da mesma.

# Leitura de tabelas e Criação de arquivos .parquet
Função "lerTabela" utilizada iterando pela lista "tabelas" onde possuímos o nome de todas as tabelas até então listadas na base de dados.

Iterando por cada item da lista "tabelas", cria-se um arquivo .parquet para cada respectiva tabela, salvos no diretório "dbfs:/ecommerce_db/" onde cada leitura do arquivo sobrescreve o arquivo .parquet no diretório, não mantendo histórico destes.

# Criação Delta Tables a partir de arquivos .parquet
Criados arquivos .parquet no repositório "ecommerce_db", itera-se arquivo a arquivo criando dataframe no formato 'parquet' e identificando as colunas de cada .parquet no dicionário "columnas" onde cada chave refere-se a uma tabela e seus valores contém uma lista com as respectivas colunas.

Consultando existência de cada delta table, cria-se uma nova delta table em caso de inexistência de tabela com o nome 'delta_{arquivo da tabela iterado}'

# Merge
A etapa de merge de dados conta com uma nova iteração por cada arquivo parquet contido no diretório "ecommerce_db".
O dicionário primaryKey conta com chaves contendo nome das delta tables e valores contendo suas respectivas chaves primárias de tabela para identificador para merge.

Por fim, esta iteração carrega cada arquivo .parquet em um dataframe Spark e em seguida realiza o merge dos dados contidos no dataframe para a respectiva delta table utilizando a funcionalidade de merge em delta lake.

- Registros contigos no .parquet e não existentes na delta table são inseridos;
- Registros existentes tanto no .parquet quanto delta table são atualizados na delta table de acordo com arquivo .parquet;
- Registros ausentes do arquivo.parquet são removidos da delta table em questão.

# Respostas questões Tarefa 6:
Questões respondidas em modelo de consulta SQL informando a resposta para cada uma.

## 🤝 Colaboradores
Alecsander Santos de Araujo
https://www.linkedin.com/in/santtosdinho/
