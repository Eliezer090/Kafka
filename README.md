# Kafka
[Full Cycle - Apache Kafka do Zero](https://www.youtube.com/watch?v=2uCEww7x4rs)
# O que é o Kafka:
- Sistema de logs "Streeaming de dados"(Banco de dados mas sem tabelas, só um log uma msg em baixo da outra), ele pega o log e guarda espera o consumer e após o consumer ler ele ainda guarda esta informação por um tempo especifico ou para sempre(Isto eu defino) isso da uma segurança maior.<br>
- Latencia de 2ms<br>
- Raplication Factor(Replicar a mesma infromação em brokers diferentes para garantir que o dado esteja sempre disponivel)<br>

## Como o kafka é extruturado: 
É separado da seguinte maneira: 
- Brokers (Que seriam os servidores Kafka ou mas maquinas no caso)
- Topic (Cada broker pode ter N topics, topics seriam nome das filas, em um e-commerce seria Carrinho por exemplo, ou podemos definir como um armário o topic)
- Partitions (Podemos ter N partitions dentro de cada topic, essas partitions seriam gavetas por exemplo de um topic)
### Producers e Consumers
Dentro da extrutura do kafka temos os Producers e os Consumers:
- Producers seriam quem gera os dados, é quem envia os dados para o kafka
- Consumers seriam os consumidores de fato deste topic, deve ser detacado aqui que o Consumer se conecta nas partitions do topic, abaixo é detalhado melhor este ponto. A quantidade de consumers deve ser relativa a quantidade de partitins que temos no topic, ex: <br>
- 1 topic=Carrinho <br>
- 3 partitions<br>
- 4 consumers do group=X<br>
- 3 consumers do group=Y
- 2 consumers do group=Z
- Conectamos os consumers ao topic Carrinho, a quantidade consumers do group=X é maior do que a partitions, então 1 desses consumers ficará sem receber dados, pois cada partition irá se conectar com 1 consumer do mesmo group se a quantidade for >=, já se conectarmos os consumers do group=Y, teremos 1 partition para cada consumer, e se conectarmos os consumers do group=Z teremos 1 consumer com 2 partitions e o outro consumer com 1 partition.

## Exeplicações em linhas gerais:
Cuidar pois o Kafka tem a questao das partições que cada topico tem, pois a partição nunca vai se comunicar com o mesmo consumer do mesmo group, é isso que a imagem abaixo diz, um Goup com varios consumers consumindo de dois topics diferentes, mas o mesmo consummer pode se comunicar com mais de uma partição:  <br>
<img src="https://github.com/Eliezer090/Kafka/blob/e5ccfbe3912041a1ffcc6d7d194d5c31670ad88f/Captura%20de%20Tela%202021-12-08%20a%CC%80s%2021.14.41.png" width="700" title="Partições e Consumers"> <br>
Ou seja o numero de consumers e topics deve ser o mesmo, se o numero de consumers ser maior que o numero de partições daquele Topic, algum consumer vai ficar sem receber dados.

## Diferença entre mensageria e streeaming de dados(Kafka):
- Mensageria:<br>
 Pedido X foi comprado pelo cliente Y que pagou com cartao B....<br>
 - Streeaming de dados(Kafka):<br>
 Auditoria de infromações, onde a infromação precisa ser distribuida para todos os consumers(Aqui pode ter mais de um) de uma forma rapida e esta informação nao pode ser perdida. Um exemplo é o PubSub que faz basicamente a mesma coisa, de distribuir a mesma mensagem par todos os consumers, kafka recebe qualquer tipo de dados mas nao substitui um banco de dados pois nao existe tabelas ele sim é um sistema de LOGS.<br>

## Onde seria util aplicar o kafka de fato:
 - Aplicar para uma comunicação de um cliente, por exemplo o cliente manda a msg para um proxy que se passa por uma api rest mas por baixo esse proxy vai mandar a requisição para o kafka.<br>
 - Comunicação entre o meu banco de dados e outras aplicações, tenho um trabalho de levar algumas informações de uma ponta para outra para isso temos o Kafka connect que faz este trabalho muito bem, abaixo tem uma imagem representando isso: <br>
 <img src="https://github.com/Eliezer090/Kafka/blob/ffe866a2a0267be83c8a0debe2e7f6b1f98c9117/Captura%20de%20Tela%202021-12-08%20a%CC%80s%2021.09.58.png" width="700" title="Kafka Connect">
