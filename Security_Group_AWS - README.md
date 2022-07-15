### O que é o Security Group da AWS?

*É um grupo de segurança que atua como um firewall virtual, controlando o tráfego que tem permissão para alcançar e deixar os recursos aos quais ele está associado. Por exemplo, depois de associar um grupo de segurança a uma instância do EC2, ele controla o tráfego de entrada e saída da instância. Ao contrário do Network ACL, as regras de security group são associadas ao nível do recurso. Isso permite a construção de regras mais granulares e funciona de forma mais integrada com um ambiente Cloud, sendo uma forma igualmente segura e amplamente utilizada. O security group também funciona tanto para inbound como para outbound, sendo que é mais comum configurar somente o inbound pela forma que o security group funciona.*

****A definição de uma regra de security group é dividida pelas seguintes partes:****

- *`Um tipo de tráfego, seja um serviço, uma porta ou um range de portas;`*
- *`Um protocolo, sendo os mais utilizados TCP ou UPD;`*
- *`Qual a origem ou destino do tráfego, que pode ser tanto um endereçamento CIDR ou outro security group;`*
- *`Uma descrição amigável.`*

#### Exemplo de um security group definindo regras bastante semelhantes das configuradas com Network ACL:

![sg-rules](https://user-images.githubusercontent.com/108905120/179172868-8a440281-8b2f-4050-a565-06d32c071bf1.png)

*Nessas regras, estamos permitindo o tráfego de qualquer rede nas portas 80 e 443 (HTTP e HTTPS), além de portas para administração dessa máquina virtual com SSH ou RDP, a partir de um bastion host. Não é preciso definir o outbound dessas conexões em um security group pois se o tráfego de entrada é permitido, o seu retorno automaticamente é permitido. Isso inclui serviços que usam portas efêmeras também.*
