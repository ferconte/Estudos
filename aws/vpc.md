### O que é VPC?

*Uma nuvem privada virtual (VPC) é uma nuvem privada segura e isolada hospedada em uma nuvem pública. Os clientes da VPC podem executar código, armazenar dados, hospedar sites e fazer qualquer outra coisa que poderiam fazer em uma nuvem privada comum, mas a nuvem privada é hospedada remotamente por um provedor de nuvem pública. As VPCs combinam a escalabilidade e a conveniência da computação em nuvem pública com o isolamento de dados da computação em nuvem privada.*

![virtual-private-cloud](https://user-images.githubusercontent.com/108905120/179183765-2a4f1847-c16e-4b32-9ea5-9a5721681509.svg)

#### Nuvem Pública:

*Uma nuvem pública é uma infraestrutura de nuvem compartilhada. Vários clientes do fornecedor de nuvem acessam essa mesma infraestrutura, embora seus dados não sejam compartilhados. Os provedores de serviços de nuvem pública incluem AWS, Google Cloud Platform e Microsoft Azure, entre outros.*

#### Nuvem Privada:

*Uma nuvem privada, no entanto, tem locatário único. Uma nuvem privada é um serviço de nuvem oferecido exclusivamente a uma organização. Uma nuvem privada virtual (VPC) é uma nuvem privada dentro de uma nuvem pública; ninguém mais compartilha a VPC com o cliente da VPC.*

### Como uma VPC é isolada em uma nuvem pública?

*Uma VPC isola os recursos de computação dos outros recursos de computação disponíveis na nuvem pública. As principais tecnologias para isolar uma VPC do restante da nuvem pública são:*

**Sub-redes**: *Uma sub-rede é um intervalo de endereços de IP dentro de uma rede que são reservados para que não fiquem disponíveis para todos dentro da rede, essencialmente dividindo parte da rede para uso privado. Em uma VPC, esses são endereços de IP privados que não podem ser acessados pela internet pública, diferentemente dos endereços de IP normais, que são visíveis publicamente.*

**VLAN**: *Uma LAN é uma rede local ou um grupo de dispositivos de computação que estão todos conectados uns aos outros sem o uso da internet. Uma VLAN é uma LAN virtual. Assim como uma sub-rede, uma VLAN é uma forma de particionar uma rede, mas o particionamento ocorre em uma camada diferente dentro do modelo OSI (camada 2 em vez da camada 3).*

**VPN**: *uma rede privada virtual (VPN) usa criptografia para criar uma rede privada por cima de uma rede pública. O tráfego da VPN passa por uma infraestrutura de internet compartilhada publicamente – roteadores, switches, etc. – mas o tráfego é embaralhado e não fica visível para ninguém.*
*Uma VPC terá uma sub-rede e uma VLAN dedicadas que só podem ser acessadas pelo cliente da VPC. Isso impede que qualquer outra pessoa na nuvem pública acesse recursos de computação na VPC – colocando efetivamente o sinal "Reservado" na mesa. O cliente da VPC se conecta via VPN à sua VPC, para que os dados que entram e saem da VPC não fiquem visíveis para outros usuários de nuvem pública.*

*Alguns provedores de VPC oferecem personalização adicional com:*

**Network Address Translation (NAT)**: *Esse recurso combina endereços de IP privados com um endereço de IP público para conexões com a internet pública. Com a NAT, um site ou aplicativo voltado para o público pode ser executado em uma VPC.*

**Configuração de rota BGP**: *Alguns provedores permitem que os clientes personalizem as tabelas de rota BGP para conectar sua VPC com sua outra infraestrutura. (Saiba como o BGP funciona).*

### Quais são as vantagens de usar uma VPC em vez de uma nuvem privada?

**Escalabilidade**: *Como uma VPC é hospedada por um provedor de nuvem pública, os clientes podem adicionar mais recursos de computação sob demanda.*

**Fácil implantação de nuvem híbrida**: *É relativamente simples conectar uma VPC a uma nuvem pública ou a uma infraestrutura local por meio da VPN. (Saiba mais sobre nuvens híbridas e suas vantagens.)*

**Melhor performance**: *Sites e aplicativos hospedados na nuvem normalmente têm uma performance melhor do que aqueles hospedados em servidores locais.*

**Melhor segurança**: *Os provedores de nuvem pública que oferecem VPCs costumam ter mais recursos para atualizar e manter a infraestrutura, especialmente para pequenas e médias empresas. Para grandes empresas ou empresas que enfrentam regulamentações de segurança de dados extremamente rígidas, isso não é tão vantajoso.*
