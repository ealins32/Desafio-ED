## Desafio Engenheiro de Dados.

### Qual o objetivo do comando cache em Spark?
O objetivo do comando cache no Spark é tornar mais eficiente e rápida as consultas e uso dos algoritmos, ocorre que a inserção de conjuntos de dados em um cache de memória, é muito útil quando os dados são acessados repetidamente, como ao consultar um pequeno conjunto de dados ou ao executar um código iterativo. Como as operações no Spark são Lazy, o cache pode ajudar a forçar esse uso.

 ### O mesmo código implementado em Spark é normalmente mais rápido que a implementação equivalente em MapReduce.  Por quê?
Isso ocorre devido a grande diferença entre os dois o MapReduce é estritamente baseado em disco, enquanto o Apache Spark usa memória e pode usar um disco para processamento. Outro ponto o MapReduce usa armazenamento persistente e o Spark usa conjuntos de dados distribuídos resilientes. O Hadoop MapReduce destina-se a dados que não cabem na memória já o Spark é capaz de executar tarefas de processamento em lote entre 10 e 100 vezes mais rápido que o MapReduce.

### Qual é a função do SparkContext?
SparkContext tem como função criar conexão transparente com o Cluster que é criada automaticamente quando se inicia o comando Shell por exemplo, ele possui os nós de execução (Executers). Podemos dizer também que o SparkContext é uma conexão padrão que o Spark cria com o Cluster.

### Explique com suas palavras o que é Resilient Distributed Datasets (RDD).
É uma arquitetura utilizada para grandes volumes de dados, são tipos de dados no qual não podemos mudar (imutável), processados em memória, mas pode ser persistido em disco. O RDD tem a característica que é chamada de Lazzy Evaluation, que são recalculados a cada operação e sua execução só começa quando realmente é necessária.

### GroupByKey é menos eficiente que reduceByKey em grandes dataset.  Por quê?
É menos eficiente porque, quando um GroupByKey é chamado em um par RDD, os dados nas partições são embaralhados na rede para formar uma chave e uma lista de valores. Essa é uma operação cara, principalmente quando se trabalha em um grande conjunto de dados. Isso também pode causar problemas quando a lista de valores combinados é muito grande para ocupar em uma partição. Nesse caso, ocorrerá um estouro de disco. GroupByKey opera em pares RDDs e é usado para agrupar todos os valores relacionados a uma determinada chave.

### Explique​ ​o​ ​que​ ​o​ ​código​ ​Scala​ ​abaixo​ ​faz. 

```python
val​​ ​​textFile​​ ​​=​​ ​​sc​.​textFile​(​"hdfs://..."​) 
val​​ ​​counts​​ ​​=​​ ​​textFile​.​flatMap​(​line​​ ​​=>​​ ​​line​.​split​(​"​ ​"​))
 ​ ​​ ​.​map​(​word​​ ​​=>​​ ​​(​word​,​​ ​​1​)) ​ ​​ ​​ ​​ ​​ ​​ ​​ ​​ ​​ ​​ ​​ ​​ ​​ ​​ ​​ ​​ ​​ ​​
   .​reduceByKey​(​_​​ ​​+​​ ​​_​) 
 counts​.​saveAsTextFile​(​"hdfs://..."​)
 ```
 
Na primeira linha vemos a leitura de um arquivo de 
texto armazenado em um HDFS, na segunda linha 
temos a quebra das linhas com o comando splip, depois temos uma redução 
criando uma unica coleção de palavras 
na sequencia temos o contador 1 para
cada palavra da lista, então é usado o ReduceByKey com operação de soma para reduzir as  
ocorrências e por fim os dados são pesistidos no HDFS.
