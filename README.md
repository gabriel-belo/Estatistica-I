# Estatistica-I
Curso básico de estatística da Alura " Estatística I: Entenda seus dados com R"

<h1>01. Qual é o tipo de seu dado?</h1>
<h3>1º tipo de dado</h3>
Dados categóricos: são dados que tem categorias difenretes e não existem comparações entre eles só são categorias diferentes

<h3>2º tipo de dado</h3>
Dados ordinal: São dados em ordem. porém não é possível mensurar a diferença entre os dados, pois é subjetivo. 
Exemplo: Um medidor de qualidade que vai de 1 a 10

<h3>3º tipo de dado</h3>
Dados intervalar: São dados em ordem e a diferença de um para outro é mensuravel
Exemplo: A medição dos graus de temperatura

<h3>4º tipo de dado</h3>
Dados racionais: São dados em ordem e a diferença de um para outro é mensuravel, poré, o 0 significa a ausência de algo.

Dependendo do  tipo de dado devemos itulizar um modelo estatístico específico

Histograma é um gráfico de frequências e quantas vezes elas se repetem
*Definição exercício: Histograma é um gráfico de barras que mostra a frequência de cada valor num conjunto de dados.

Devemos também entender a distribuição dos dados para saber qual será o modelo aplicado

<h1>02. Primeiros passos com R</h1>
Para pesquisar a documentação de alguma função no R usamos ?nome_função
para criar listas: lista <- c()
para criar variáveis usamos: variavel<- 5

<h1>0.3 Média, Mediana e Moda</h1>
Média aritmética soma todos os ítens e divide pela quantidade de ítens.
A média aritmética nem sempre será a forma mais eficiente de encontrar a média pois ela pode ter falhas dependendo do tipo de dado, no caso de um dado ordinário grande parte das notas podem ser muito baixar porém poucas notas altas podem elevar muito a media fazendo com que modifique a perspectiva.
A média aritmética é adequada para distribuições estáveis 
A média não é muito adequado para números ordinais.
Por isso devemos conhecer a distribuição para saber o melhor método.

A mediana é outra forma de encontrar a tendência central, mediana é o elemento que está localizado no meio da distribuição, quando ela está ordenada.
Mediana com números ímpars fazemos a divsão da distribuição no meio por exemplo com 7 números dividimos em dois grupos os anteriores ao número da media e os posteriores a mediana.
No caso de um grupo de numéros que de par, podemos escolher os dois números que estão no meio e calcular a média aritmética ou escolher o número mais acima ou mais abaixo.
A mediana é menos sucetivel a pontos extremos(outliers).

Moda é o elemento que mais se repete na distribuição 
Exemplo: Em uma lista com os números 1,1,2,2,2,2,3,3,5,5,5
Os números 1 e 3 se repetem duas vezes, o 5 repete três vezes e o 2 repete 4 vezes. Então a moda é 2.

Em destribuições homogenias a mediana, moda e media aritmética tendem a ter o mesmo resultado.

Em números odrinais usar mediana ou moda.
Usar média aritmética em dados intervalares, porém analisar se não existem números muito fora da curva pois podem fazer com que distorça o resultado. 

<h1>0.4 Praticando; Média, Mediana e Moda</h1>
A função para gerar a média aritmética de uma série de valores é mean()
Para gerar a mediana usamos a função median()
Para gerar a moda não possuimos uma função, porém podemos criar uma para gerar a moda.
mode <- function(x){
  ux <- unique(x)
  ux[which.max(tabulate(match(x,ux)))]
}

moda <- mode(lista)
print(moda)


Para verificar se a distribuição é normal ou não faremos um teste de hipótese usamos shapiro.test(numeros). E iremosm receber de volta vários valores se p-value for menor que 0.05 a distribuição não é normal.

Podemos receber muitos valores também através da função summary(), teremos como resposta o valor mínimo e máximo a mediana e a média e  primeiro quartil e terceiro quartil 

Como calcular as tendências centrais(moda, media e mediana) com a biblioteca pandas do python:
import pandas as pd
df=  pd.DataFrame([dados])
df.mean()
df.median()
df.mode() #moda

<h1>05. Variabilidade, dispersão dos dados, Outlers e Quartis</h1>
Podemos ter situações em quecomparando duas estruturas de dados com valores diferentes chegamos ao mesmo valor para media, moda e mediana, porém podemos perceber qual das duas estruturas tem uma media de valores mais próximos e qual chegou ao mesmo valor para as tendências centrais através de valores muito distantes(valores muito baixos e valores muito altos). Podemos fazer isso através do calculo da amplitude pegando o maior e o menor valor das estruturas de dados e subtraindo eles, encontrando assim o desvio. Porém esta forma é sensivel ao dados, senso assim fácil de entregar algo que não represente a verdade, pois podemos ter exceções.
Para não cair nesses desviosiremos fazer uma divisão por quartis ou análise de quartil. Para fazer isso iremos dividir a distribuição em três partes, 25% do começo, 25% do fim e deicar os 50% do meio, caso de um número quebrado na hora de dividir iremos arredondar.
Com a divisão por quartil pegamos o centro que é onde tende a ter a informação de forma mais realista.
Exemplo:
3,3,6,7,7,10,10,10,11,13,30

Neste caso temos 3,3 e 6 como 1º quartil e 11, 13 e 30 como 3º quartil. Pegamos os valores 3 e 11 e multiplicamos e dividimos por 4 dando então 8... que arredondando da 9.
Então pegamos os valores do meio e buscamos a mediana, moda ou media.
Podemos utilizar o boxplot para termos uma ideia de como esta a distribuição, alguns ainda acrescentam a mediana ao boxplot, podemos então colocar o boxplot de duas estrutras de dados e analisar.
No boxplot contemos as informações da mediana, primeiro quartil, terceiro quartil, maior e menor elementos da distribuição.

<h1>06. Praticando: boxplot</h1>
Para gerar um boxplot só precisamos usar a função boxplot() 
Para gerar em um arquivo para que possa utilizar depois usamos a função png(file=parâmetro)
Exemplo: png(file="/Users/alura/bloxpot.png", width=700, height= 700)
Usamos o width e height para colocar comprimento e altura em pixels.
caso faça essa definição ao tentar gerar depois ele não aparecera na tela e já será gerado automaticamente e gerado no caminho indicado, usamos o dev.off() para enviar o buffer para o arquivo da imagem previamente configurado.
se dermos o comando open boxplot.png ele irá gerar o boxplot salvo na tela

<h1>07. Variância e Desvio Padrão</h1>
A media por si só não fala o quanto a distribuição esta espalhada, mas dá a tendência central
Porém para fazer a comparação no exemplo é necessário tem o conhecimento da distribuição para saber qual tem melhor frequência.
Tentamos através das amplitudes porém os outliers atrapalharam, então fomos para a distribuição por quartis para retirar os outliers.
Para calcular a media da dispersão dos dados iremos calcular cada ponto da media e depois calcular a media desses número para encontrar.
Exemplo:
1 2 9
media=4
(4-1)+(4-2)+(4-9)/3
3+2-5/3
0/3=0
Para eleminar esses números negativos e fazer com que cada ponto tenha valor sobre o cálculo iremos colocar os números ao quadrado
(4-1)²+(4-2)²+(4-9)²/3
3²+2²-5²/3
9+4+25/3
38/3
12,6... arredondando é 13
agora como os números foram elevados ao quadrado iremos pegar a raiz de 13
raiz de 13 +- = 3.5
Esse 3.5 quer dizer que na media dessa distribuição os números estão espelhados por 3.5 para ambos os lados.
O 3.5 é conhecido como desvio padrão que mostra como os números estão dispersos
O desvio padrão é uma medida estatística que indica o grau de dispersão dos dados em relação à média. Ou seja, ele mostra o quanto os valores de um conjunto de dados variam em torno da média.
O desvio padrão tenta achar a distância de um ponto em relação a média, faz então o calculo de cada ponto em relação a media e chega a media de todos os desvios
Quanto maior o desvio menor a constância e vice versa

A variância é expressa na unidade dos dados elevada ao quadrado.
O desvio padrão é a raiz quadrada da variância, o que traz os valores para a mesma unidade dos dados originais.

<h1>08. Praticando: Desvio Padrão</h1>
Para encontrar a variância no R usamos a função var()
Para chegar ao desvio padrão usamos a função sqrt() que pega a raiz ao quadrado da variância ou podemos usar a função sd para chegar ao desvio padrão também

Como ler dados de um arquivo?
Para ler o arquivo usamos a função read. seguida do tipo de arquivo, por exemplo read.csv(file="/Users/alura/numeros.csv")
Podemos então armazenar em uma variável e trabalhar com os dados
Para apresentar uma coluna fazer por exemplo: nome_variavel$nome_da_coluna
Podemos fazer várias coisas então por exemplo gerar o histograma de uma coluna assim: hist(nome_variavel$nome_da_coluna)

<h1>09. População X Amostra: Pensando em um estudo</h1>
População é o conjunto total de pessoas que queremos estudar
Amostra é um conjunto de pessoas retiradas da população, então o estudo é feito dentro da amostra e generalizamos.
A amostra deve ser aleatória(randômica) todos devem ter a mesma chance de serem escolhidos, os vies podem limitar ou fazer com que pessoas em certas situações sejam escolhidas.
Outra forma de gerar a amostra é através de uma amostra estratificada está funciona através do conhecimento de que existem grupos dentro da população então buscamos de forma aleatória dentro dos grupos.
A média da amostra é igual a média da população
A variância é como os números estão espalhados, para calcular a variância faziamos a diferença de cada número para a media os somavamos e dividiamos pela quantidade de elementos.
Para calcular a variancia da amostra iremos fazer o mesmo porém iremos subtrair a quantidade de elementos por 1, isso é feito pois o resultado será maior dividido por um número maior do que por um número menor, a variância da população é maior que a da amostra.
A variância da população é maior que a da amostra. 

<h1>10. Praticando graus de liberdade</h1>
Exemplo de graus de liberdade:
Temos uma soma de 4 variaveis a,b,c,d o resultado final da 10; para as variaveis a,b,c podemoster qualquer valor pois a variavel d pode ter um número que faça com que o resultado de 10
Então de 4 números, podemos escolher 3, portanto, 3 graus de liberdade.
Os graus de liberdade (GL) representam o número de valores independentes que podem variar em um cálculo estatístico sem que as restrições sejam violadas.
Se a amostra é grande, a variância da população e da amistra serão parecidas.
O n-1 na fórmula para a amostra só faz sentido para pequenas amostras, grandes amostrar acabam chegando a um valor similar ao da população.
Exemplo:
Soma = 240
n=4 
população 

A diferença entre dividir por 𝑁 (no caso da população) e por 𝑛−1 (no caso da amostra) no cálculo da variância se deve a um conceito chamado viés da amostra e ao grau de liberdade.
Quando calculamos a variância da população inteira, utilizamos N porque temos acesso a todos os valores do conjunto de dados. Assim, a média (μ) é exata, e não há incerteza.
Quando usamos apenas uma amostra da população, não conhecemos a média real (𝜇) da população, apenas a média amostral (x).
O problema é que a média amostral tende a subestimar a variabilidade da população.
Se usássemos apenas n no denominador, a variância calculada seria, em média, menor do que a verdadeira variância da população.
Por isso, dividimos por 𝑛−1 para corrigir esse viés. Essa correção é chamada de Correção de Bessel.
Essa correção faz com que a variância amostral seja uma estimativa não tendenciosa da variância populacional.
Quando calculamos a variância amostral, usamos a média da amostra (𝑥) em vez da média populacional (𝜇). Porém, a média amostral já foi calculada a partir dos próprios dados e impõe uma restrição aos valores individuais.
Como resultado, perdemos um grau de liberdade, porque um dos valores já está "preso" pela média.
Temos em torno de 3 desvios padrões para cada lado.

<h1>11. Diminuindo o erro: Intervalo de confiança</h1>
Como temos uma diferença entre a média da amostra e a média da população, então para não ter uma margem grande de erro damos um intervalo. 
Por exemplo:
Se a média for 7 da amostra, iremos dar um intervalo de 6 a 8(intervalo de confiança) e temos 95%(nivel de confiança) de certeza.
Quanto maior o nível de confiança, maior é o intervalo de confiança.
85% é um nível de confiança comum 

<h1>12. Praticando: Intervalo de Confiança</h1>
Não temos uma função padrão para calcular o teste de confiança, então usaremos um teste de hipótese que tem o teste de confiança como saida

https://www.ifmg.edu.br/conselheirolafaiete/noticias/anexos-noticias/apostila-introducao-a-estatistica-ifmg-cl.pdf
