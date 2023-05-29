Trabalho de aplicação de Mapa Kohonen, Rede Bayesiana e Método Fuzzy
Professor: Cesar Alberto Penz

Alexsandro Gehlen
Rodrigo Abel Farias de Souza







































Florianópolis
2023
Interrupção de ventilação mecânica assistida





1º Caso:

Normalização
nenhuma
Função vizinhança
gaussian
Tamanho dos mapas
10x10
Topologias
hexagonal





Avaliação
	Foram montadas cinco configurações para o Mapa de Kohonen classificar a retirada de respiradores. Na segunda configuração ela foi reduzida pela metade em relação à primeira, mas alguns neurônios associadas ao valor “sim” (azul) ficaram entre os vermelhos, algo que pode ser um problema na hora de classificar os dados de testes. Na terceira opção chegamos a uma matriz 3x3, mas a separação não é tão visível. Na quarta foi aumentada suas larguras com tamanhos diferentes, gerando regiões em que podem ser encontrados neurônios azuis e vermelhos. No quinto caso foi alterado a largura gerando assim uma matriz com todos os neurônios vencedores associados aos casos de treinamento mas apresentou muita sobreposição de classificação. O primeiro caso foi escolhido pois mesmo sendo o maior grid apresentou uma separação mais interessante como é observado na u-matriz.
	Todas as configurações receberam os dados de teste, foi escolhido o primeiro caso pois na u-matrix de treinamento ele tem uma separação bem visível. 


Como é possível verificar na imagem acima, teve casos do treinamento que apresentaram valores numéricos condizentes com falhas mas que foram um sucesso na realidade criando incongruência com a u-matriz. Verificando um caso de teste que obteve o neurônio vencedor 21 e era uma falha percebe-se que há um limiar de sucesso e falha nesta área. Assumindo apenas este caso de teste como não classificado corretamente o mapa apresentou acurácia de 88,9%.
	Os dados de teste foram passados novamente na primeira vez sem a coluna  VT, e apresentou mais um caso que na realidade é um sucesso mas se encontra no limiar da classificação (Acurácia: 77,8%), na segunda sem a coluna NIF (Acurácia: 66,7%) e por último sem a coluna RR, isso não alterou a acurácia que se manteve em 88,9%. Um detalhe significativo é que para as análises desta segunda atividade foi utilizado o Octave para execução dos algoritmos, podendo apresentar diferenças se comparado a outras ferramentas como o MatLab.


Interrupção de ventilação mecânica assistida com Naive-Bayes

	Para este caso o Naive-Bayes foi utilizado como ferramenta de classificação dos casos onde se obteve sucesso ou falha na retirada da ventilação mecânica do paciente. Para implementação do algoritmo de Naive-Bayes foi utilizado a linguagem python e a biblioteca de aprendizado de máquina scikit-learn.
	O dataset é o mesmo utilizado no trabalho do mapa de kohonen, os dados foram separados em 70% para treinamento e 30% para testes e seu rótulo de classificação foi mudado de S para 0 e F para 1. A distribuição foi dada pela Gaussiana. Os dados foram normalizados para treinar e testar o modelo. 
	Os resultados foram avaliados por algumas métricas, e demonstraram uma acurácia de 88.9%, uma precisão de 100%, um recall de 0.75% e um F1 de 86%. Esses dados foram obtidos através da matriz de confusão, nela é possível observar que teve apenas um falso positivo.


	O único resultado que classificou erroneamente como falso positivo foi um caso onde a probabilidade estava 52.49% e 47.50% que os dois estão muito próximos podendo levar a falha como ocorreu. Na imagem da tabela abaixo é possível observar as probabilidades, como o modelo classificou e como é a classificação do dataset.


	Para melhoria poderiam ser testados com outras distribuições e comparações de resultados, diferente de outras ferramentas não foi necessário configurar os limites possibilitando implementar um modelo, mas para melhoria do modelo em dataset' s maiores seria necessário entender melhor do problema e a importância de cada dado.














Interrupção de ventilação mecânica assistida com método Fuzzy

Utilizando a mesma base de dados sobre ventilação mecânica e o método Fuzzy foi utilizado como ferramenta de classificação dos casos onde se obteve sucesso ou falha na retirada da ventilação mecânica do paciente. Para implementação do algoritmo de Fuzzy foi utilizado a linguagem python e as bibliotecas de aprendizado de máquina Skfuzzy para o método e scikit-learn para obtenção das métricas do método.
	As variáveis escolhidas para classificação de sucesso ou falha da interrupção da ventilação mecânica foi o módulo de NIF (Negative Inspiratory Force) e RSBI (Rapid Shallow Breathing Index) que foi obtido a partir dos dados fornecidos no dataset já citado anteriormente. Os gráficos de pertinência da variáveis NIF, RSBI e Ação a ser tomada seguem respectivamente:


Baseado nas fontes disponibilizadas para o trabalho foi assumido que um módulo de NIF menor que 25 seria considerado um valor baixo, e que a chance de sucesso depois da interrupção do procedimento seria também baixo. Já para valores acima de 25 são considerados altos e associados a chances maiores de sucesso.

Os intervalos assumidos para valores considerados baixos para RSBI foram abaixo de 105, e neste caso a chance de sucesso na interrupção do procedimento é maior, já para valores de RSBI maior que 105 a chance de falha aumenta.

Quanto a ação a ser tomada foi criado um intervalo de 0 a 1 em que zero é falha e um sucesso, uma solução para quantificar a variável qualitativa. A divisão foi simétrica assumindo o ponto de virada 0.5. Para as três variáveis foram criados estados baixo, médio e alto.
	As regras de controle assumidas foram apenas as condições discutidas para cada variável. O módulo de NIF alto é associado a ação de interrupção com alta taxa de sucesso (Action = 1), e o inverso também é válido. No caso de valores altos de RSBI associa-se a ação de interrupção com baixa taxa de sucesso (Action = 0),e o inverso também é válido.
A partir do dataset já categorizado fornecido foram encontrados casos em que mesmo os valores estando dentro dos intervalos condizentes o resultado não foi o esperado. O exemplo que segue apresenta um valor de NIF igual a -30 e RSBI de 34, ambos valores que estão associados a uma chance maior de sucesso, obtendo um valor de Action de 0.82, e mesmo assim é uma falha de acordo com dataset.

As métricas para avaliação do método utilizados no dataset de treinamento e validação demonstraram uma acurácia de 76.7%, uma precisão de 70%, um recall de 93.3% e um F1 de 80%. Segue a matriz confusão dos dados de treinamento e validação fornecidos, sendo que para criação desta foi considerado que valores de Action maiores que 0.5 seriam considerados como sucesso e menores que 0.5 como falha.

Os resultados das métricas podem apresentar valores mais interessantes com a utilização de mais variáveis pertinentes para predição do sucesso ou falha da interrupção do procedimento de ventilação mecânica, outro caminho que pode ser abordado é um estudo mais aprofundado das influências destas variáveis para criação de regras mais representativas para controle de decisão do método.


Avaliação de desempenho dos diferentes métodos

	Foram aplicados diferentes métodos de resolução para o mesmo problema, cada qual com sua metodologia de implementação e execução. As métricas utilizadas para comparar em todos casos foi a acurácia que os modelos de mapa de Kohonen e Naive-Bayes apresentaram desempenho equivalente de 88.9%, já o Fuzzy teve um desempenho aquém apresentando um valor de 76.7%. 
Devido a natureza arbitrária da definição das regras do modelo de Fuzzy este pode apresentar um desempenho mais interessante com uma base de conhecimento maior e com variáveis mais diversificadas que são pertinentes ao problema. Na implementação do naive-bayes foi possível ter um grau de abstração maior devido a utilização da biblioteca scikit-learn. Já no mapa de Kohonen foi utilizado Matlab na qual foram testados algumas funções de vizinhança e tamanho da matriz até chegar nos resultados satisfatórios.
