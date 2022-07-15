## O que é um IP?

*Um endereço IP é uma sequência de números separados por pontos. O endereço IP é representado por um conjunto de quatro números: por exemplo, 192.158.1.38. Cada número do conjunto pode variar entre 0 e 255. Ou seja, o intervalo de endereçamento IP vai de 0.0.0.0 a 255.255.255.255.*

## Tipos de endereços IP:

*Existem diferentes categorias de endereços IP e, em cada categoria, diferentes tipos. Cada pessoa ou empresa com um plano de serviços de Internet terá dois tipos de endereços IP: endereço IP privado e público. Os termos público e privado referem-se ao local da rede, ou seja, um endereço IP privado é usado dentro de uma rede, enquanto o público é usado fora de uma rede.*

### Endereços IP privados:

*Todo dispositivo (computadores, smartphones, tablets, etc.) que se conecta à rede de Internet tem um endereço IP privado.O roteador gera endereços IP privados que são identificadores exclusivos de cada dispositivo e que os diferencia na rede.*


### Endereços IP públicos:

*O endereço IP público é o principal endereço associado à toda a sua rede. Embora cada dispositivo conectado tenha um endereço IP, eles também estão incluídos na rede IP principal da sua rede.Seu endereço IP público é o endereço que todos os dispositivos fora da sua rede de Internet usarão pera reconhecer sua rede.*

##### Os endereços IP públicos têm dois formatos: dinâmico e estático.

*```Os endereços IP dinâmicos mudam de forma automática e regularmente.```*

*```Os endereços estáticos permanecem consistentes. Uma vez que a rede atribui um endereço IP, ele permanece o mesmo.```*

## O que é uma sub-rede?

*Uma sub-rede, é uma rede dentro de outra rede. As sub-redes tornam as redes mais eficientes. Por meio da sub-rede, o tráfego da rede pode percorrer uma distância menor sem passar por roteadores desnecessários para chegar ao seu destino. Como os endereços de IP são criados torna relativamente simples para os roteadores da internet encontrar a rede correta para encaminhar os dados. Um endereço de IP se limita a indicar a rede e o endereço do dispositivo, os endereços de IP não podem ser usados para indicar para qual sub-rede um pacote de IP deve ser encaminhado. Roteadores dentro de uma rede usam o que se chama de máscara de sub-rede para classificar os dados em sub-redes.*

![subnet-diagram](https://user-images.githubusercontent.com/108905120/179135824-d694a3a7-a46c-4193-b966-99d2668f2367.svg)

## O que é uma máscara de sub-rede?

*Uma máscara de sub-rede é como um endereço de IP, mas apenas para uso interno dentro de uma rede. Os roteadores usam máscaras de sub-rede para encaminhar pacotes de dados para o lugar certo. As máscaras de sub-rede não são indicadas dentro dos pacotes de dados que atravessam a internet. Esses pacotes indicam apenas o endereço de IP de destino, que um roteador irá combinar com uma sub-rede.*
