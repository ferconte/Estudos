### O que é EC2?

*Ele é um serviço de computação onde a plataforma vende o poder de processamento, armazenamento e transferência de informações como serviço. Ele faz parte do nível de serviço IaaS (Infraestrutura como serviço) e seu recurso central são as instâncias.*

### O que é instância?

*As instâncias são máquinas virtuais criadas dentro da infraestrutura da AWS onde podemos montar nossos servidores, processar informações ou realizar outras tarefas. A principal característica é a autonomia, podemos realizar qualquer tarefa administrativa dentro do sistema operacional das nossas instâncias, desde coisas mais simples até elementos mais avançados como instalação de programas, serviços e alterações de configurações.*

### Criando a primeira instância.

*Dentro do serviço da AWS primeira coisa que precisamos fazer é acessar a página do serviço EC2. No menu superior do console web clique em Services > EC2:*

![image](https://user-images.githubusercontent.com/108905120/179623311-3fe95452-6c8c-47a8-b320-ce09b0aa4264.png)

#### Passo 1:

*Escolher o nome:*

![image](https://user-images.githubusercontent.com/108905120/179625293-8f889721-82ca-4a51-82e0-c0d8be83f0de.png)

#### Passo 2:

*Escolher a imagem do sistema:*

![image](https://user-images.githubusercontent.com/108905120/179626858-e5ed22ad-c9ce-4cc1-b6b2-758380bff713.png)


#### Passo 3: 

*Escolher tipo de instância:*

![image](https://user-images.githubusercontent.com/108905120/179627411-70c14e00-2b4a-48bd-a3d5-deef8eede7d5.png)

#### Passo 4:

*Ele vai pedir para selecionar uma chave de acesso que funciona como se fosse a senha para acessar sua máquina. Selecione a opção Create a new key pair, coloque uma descrição e clique em Download Key Pair... Após baixado, guardar em um local seguro a chave, e utilizar a mesma nesse procedimento selecionando ela:*

![image](https://user-images.githubusercontent.com/108905120/179629378-6c5c6ad7-2d9e-4e81-a5c3-75b8f0bec274.png)

#### Passo 5:

*Selecionar o tipo grupo do segurity group se houver algum criado, ou criar um grupo default e dependendo o tipo de configuração utilizar SSH, podendo selecionar HTTP ou HTTPs (podendo ser público ou privado!):*

![image](https://user-images.githubusercontent.com/108905120/179629840-38c613c6-9726-4903-967e-38907fd240f9.png)

#### Acessando a máquina:

*Se a sua instância utilizar o sistema operacional Linux o acesso é feito via SSH. Se a instância usar o Windows deve ser feita via RDP. Basta selecionar a instância na lista e clicar em Connect que a própria AWS te informa o procedimento para acesso:*

![lista-de-instancias-do-ec2](https://user-images.githubusercontent.com/108905120/179630270-681ddfda-890c-4524-ad3d-f677c9ac3e0d.png)

*Informações de acesso:*

![informacoes-de-conexao-do-ec2](https://user-images.githubusercontent.com/108905120/179630315-1eec7257-9f52-498b-a32d-d08999b989f1.png)

```Se a máquina local for Linux ou Mac, basta executar os comandos acima via terminal na pasta onde baixou a chave.```

```Se a máquina local for Windows, precisará usar um cliente de SSH próprio.```

#### Finalizando:

*O EC2 possui uma série de facilidades e ferramentas que permitem o gerenciamento de forma muito profissional da estrutura em nuvem. É possível criar diversos volumes para uma mesma máquina, instalar sistemas operacionais pré-configurados com AWS Marketplace e muito outros detalhes. A Amazon AWS possui um ecossistema completo em serviços de computação em nuvem, temos artigos abordando cada um deles, como o Amazon S3, Amazon Lambda e Aurora.*
