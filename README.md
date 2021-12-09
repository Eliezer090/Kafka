# Kafka
[Full Cycle - Apache Kafka do Zero](https://www.youtube.com/watch?v=2uCEww7x4rs)
# O que é o Kafka:
- Sistema de logs "Streeaming de dados"(Banco de dados mas sem tabelas, só um log uma msg em baixo da outra), ele pega o log e guarda espera o consumer e após o consumer ler ele ainda guarda esta informação por um tempo especifico ou para sempre(Isto eu defino) isso da uma segurança maior.<br>
- Latencia de 2ms<br>
- Raplication Factor(Replicar a mesma infromação em brokers diferentes para garantir que o dado esteja sempre disponivel)<br>

Exemplo entre mensageria e streeaming de dados(Kafka):<br>
- Mensageria:<br>
 Pedido X foi comprado pelo cliente Y que pagou com cartao B....<br>
 - Streeaming de dados(Kafka):<br>
 Auditoria de infromações, onde a infromação precisa ser distribuida para todos os consumers(Aqui pode ter mais de um) de uma forma rapida e esta informação nao pode ser perdida. Um exemplo é o PubSub que faz basicamente a mesma coisa, de distribuir a mesma mensagem par todos os consumers, kafka recebe qualquer tipo de dados mas nao substitui um banco de dados pois nao existe tabelas ele sim é um sistema de LOGS.<br>

Cuidar pois o Kafka tem a questao das partições que cada topico tem, pois a partição nunca vai se comunicar com o mesmo consumer do mesmo group, é isso que a imagem abaixo diz, um Goup com varios consumers consumindo de dois topics diferentes, mas o mesmo consummer pode se comunicar com mais de uma partição:  <br>
<img src="https://github.com/Eliezer090/Kafka/blob/e5ccfbe3912041a1ffcc6d7d194d5c31670ad88f/Captura%20de%20Tela%202021-12-08%20a%CC%80s%2021.14.41.png" width="700" title="Partições e Consumers"> <br>
Ou seja o numero de consumers e topics deve ser o mesmo, se o numero de consumers ser maior que o numero de partições daquele Topic, algum consumer vai ficar sem receber dados.
## Onde seria util aplicar o kafka de fato:
 - Aplicar para uma comunicação de um cliente, por exemplo o cliente manda a msg para um proxy que se passa por uma api rest mas por baixo esse proxy vai mandar a requisição para o kafka.<br>
 - Comunicação entre o meu banco de dados e outras aplicações, tenho um trabalho de levar algumas informações de uma ponta para outra para isso temos o Kafka connect que faz este trabalho muito bem, abaixo tem uma imagem representando isso: <br>
 <img src="https://github.com/Eliezer090/Kafka/blob/ffe866a2a0267be83c8a0debe2e7f6b1f98c9117/Captura%20de%20Tela%202021-12-08%20a%CC%80s%2021.09.58.png" width="700" title="Kafka Connect">




