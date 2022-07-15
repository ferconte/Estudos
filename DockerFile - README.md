### O que é o Dockerfile?

*É responsável por criar nossas imagens. Podemos dizer que ele é a receita que essa imagem vai seguir. É com esse arquivo que podemos gerar o build e criar o container a partir dele. Para criar um Dockerfile é simples, basta criar um arquivo com o nome ```Dockerfile```.*

*Para gerar a imagem a partir do Dockerfile, executamos o comando abaixo no mesmo local que o arquivo se encontra:*

```docker build -t nome_da_imagem```

*Para criar o container a partir dessa imagem construída, podemos executar o comando:*

```docker run nome_da_imagem```

### FROM:

*Instrução obrigatória que indica qual imagem vai ser utilizada como ponto de partida. Podemos  criar uma imagem a partir de uma imagem do Node.js ou um sistema Linux usando uma imagem do Ubuntu e assim por diante. É possível criar sua própria imagem usando a instrução ```FROM scratch```.*

```FROM node:12-alpine```

*O comando acima indica que será criado uma imagem com `Node.js`.*

### RUN:

*Serve para executar comandos no processo de montagem da imagem que estamos construindo no Dockerfile, ele é executado durante o build (construção da imagem) e não durante a construção do container. Em um Dockerfile é possível ter mais de um comando RUN.*

```FROM node:alpine

WORKDIR /usr/app

RUN npm init -y
RUN npm install cowsay
RUN npx cowsay Hello Docker

RUN cat package.json
```

*Quando rodamos o comando abaixo, podemos ver o log de cada RUN sendo executado no processo de criação da imagem:*

```docker build -t nodej/nodej .```

*Resultado:*

```❯ docker build -t nodej/nodej .
Sending build context to Docker daemon  3.072kB
Step 1/6 : FROM node:alpine
 ---> 0f2c18cef5d3
Step 2/6 : WORKDIR /usr/app
 ---> Using cache
 ---> 0399f14efe3b
Step 3/6 : **RUN npm init -y**
 ---> Using cache
 ---> da2345d90786
Step 4/6 : **RUN npm install cowsay**
 ---> Using cache
 ---> bf6c1a19a89a
Step 5/6 : **RUN npx cowsay Hello Fernando**
 ---> Running in 78f5486fa633
 __________________
< Hello Fernando >
 ------------------
        \\   ^__^
         \\  (oo)\\_______
            (__)\\       )\\/\\
                ||----w |
                ||     ||
Removing intermediate container 78f5486fa633
 ---> 02d9013dbf0b
Step 6/6 : **RUN cat package.json**
 ---> Running in 675e768b4b16
{
  "name": "app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \\"Error: no test specified\\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cowsay": "^1.4.0"
  }
}
Removing intermediate container 675e768b4b16
 ---> 260e87152b92
Successfully built 260e87152b92
Successfully tagged nodej/nodej:latest
```
### CMD:

*Diferente do RUN, o CMD executa apenas na criação do container e não no build da imagem. Deve ser único no Dockerfile.*

```FROM node:alpine

WORKDIR /usr/app

RUN npm init -y
RUN npm install cowsay
RUN npx cowsay Hello Rocketseat

RUN cat package.json

CMD npm start
```
*Execute o comando abaixo para recriar a imagem:*

```docker build -t nodej/nodej``` 

*Depois rode o comando abaixo para criar o container:*

```docker run -t nodej/nodej```

*O comando vai criar a imagem e dentro do container será executado o npm start, porém no package.json não foi definido no script start, mas perceba que o CMD executou apenas no container e não na construção da imagem. E o log do erro só apareceu quando criamos o container.*

```> docker run -t nodej/nodej   
npm ERR! missing script: start
npm ERR! A complete log of this run can be found in:
npm ERR!     /root/.npm/_logs/2020-08-20T17_40_32_268Z-debug.log
```
### EXPOSE:

*Instrução que informa qual porta deverá ser liberada. EXPOSE não é um comando que libera a porta, ele serve para ficar documentado no Dockerfile quais portas deverão ser liberadas ao criar o container. Para efetivamente liberar a porta é preciso passar o parâmetro ```-p```  no comando docker run, vamos ver a seguir:*

```FROM node:alpine

WORKDIR /usr/app

RUN npm init -y
RUN npm install cowsay
RUN npx cowsay Hello Rocketseat

RUN cat package.json

EXPOSE 3000 ## informa que deverá ser liberado a porta 3000 na criação do container

CMD npm start
```
*Execute o comando abaixo para criar o container e liberar a porta ```3000```:*

```docker run -p 3000:3000 -d nodej/nodej```

*Para liberar a porta usamos o parâmetro ```-p 3000:3000```. Está sendo realizado também o redirecionamento de portas, onde o primeiro parâmetro ```3000``` é a porta do host e o segundo ```:3000``` é a porta do  container. Isto é, toda vez que o host receber uma requisição na porta ```3000```, o container irá ouvir a requisição na porta ```3000``` também.*

![dockerfile-rocketseat-exemplo-expose](https://user-images.githubusercontent.com/108905120/179179248-884f4dd9-9406-4430-913f-e621865ddb82.png)
<sup>Liberando portas na aplicação: Porta 3000 Host e :3000 Container.</sup>

*Podemos liberar portas TCP e UDP, por padrão, quando não é especificado /tcp ou /udp, é liberado a porta TCP.*

```docker run -p 80:80/tcp -p 80:80/udp ...```

*Por padrão, a porta tcp é liberada quando não é especificado o protocolo, exemplo:*

```docker run -p 8080:80```

### COPY e ADD:

*Comandos para copiar arquivos e pastas de um lugar específico na máquina local para uma pasta no container. Diferença é que ```ADD``` copia arquivos remotos para alguma pasta na imagem e também pode copiar arquivos compactados (``tar.gz``) que serão descompactados na imagem automaticamente.*
Por questões de semântica, sempre utilize ```COPY``` para copiar arquivos e pastas locais e ```ADD``` para arquivos remotos ou compactados. Utilize o ```ADD``` se realmente for necessário. Leia as boas práticas sobre ```COPY``` e ```ADD```.

#### Exemplos:

*Se quiser acompanhar em sua máquina, faça os seguintes procedimentos abaixo:*

- ```COPY```

*Digite no terminal dentro de um diretório para criar um projeto com ```Node.js```:*

```yarn init -y```

*Altere o ```package.json```:*

```{
  "name": "docker-node",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "keywords": [],
  "author": "",
  "license": "MIT"
}
```
*Crie o arquivo ```index.js``` na raiz do projeto com o seguinte conteúdo:*

```console.log("Qual é a soma de 2 + 2: ", 4);```

*Crie o arquivo Dockerfile na raiz do projeto:*

```FROM node:alpine

WORKDIR /usr/app

COPY package.json ./
COPY index.js ./

RUN npm install 

RUN cat package.json

RUN npm start

EXPOSE 3000

# CMD npm start
```
*Execute o comando abaixo no terminal e observe o log:*

```docker build -t nodej/nodej```

*No final será impresso:*

```Qual é a soma de 2 + 2 = 4```

- ```ADD```

*Exemplo com o comando ```ADD```:*

```FROM ubuntu:18.04

RUN mkdir /myfolder

WORKDIR /myfolder

ADD /sample.tar.gz ./

RUN ls  ## listando arquivos

RUN ls project

RUN ls -la

RUN echo "FIM"
```
*Execute o comando abaixo e observe o log:*

```docker build -t nodej/nodej```

*Será adicionado um arquivo compactado da máquina do host para o container recém criado dentro da pasta ```myfolder```, em seguida o arquivo será descompactado automaticamente.*

### VOLUME:

*Quando adicionamos ```VOLUME``` no Dockerfile estamos informando um ponto de montagem, criando uma pasta que ficará disponível entre o container e o host.*

```FROM ubuntu:18.04

RUN mkdir /minha_pasta
RUN echo "hello world" > /minha_pasta/hello.txt

VOLUME /minha_pasta
```
*Dockerfile acima define a utilização da imagem do ubuntu:18.04, cria uma pasta chamada ```minha_pasta``` e depois cria um arquivo ```hello.txt``` com o conteúdo "```hello world```" dentro da pasta, por fim é disponibilizado o ```VOLUME``` /minha_pasta``` para que o host tenha acesso.*

*Podemos fazer espalhamento do ```Volume``` conforme podemos ver neste post.*

### WORKDIR:

*Define uma pasta dentro do container onde os comandos serão executados.*

```FROM node:alpine

WORKDIR /usr/app

COPY package.json ./

RUN npm install

CMD npm start
```
*Estamos definindo que na pasta ```usr/app``` serão executados os comandos seguintes, o arquivo ```package.json``` será copiado do host para ```user/app```, inclusive o comando ```RUN npm install``` será executado dentro do contexto definido no ```WORKDIR```.*

### USER:

Podemos alterar os usuários para executar os comandos. No exemplo abaixo defini o usuário node para executar os comandos e, como não precisa de privilégios de super usuário (root), podemos usar usuário sem tantos privilégios.

```FROM node:alpine

USER node ## definindo o usuário que realizar os comandos

RUN whoami ## qual usuário está usando o terminal, será impresso node

WORKDIR /usr/app

COPY package.json ./

RUN npm install

CMD npm start
```

### Conclusão:

*Interessante observar a flexibilidade que temos quando criamos nossas imagens e containers com Docker.* 

Vimos os principais comandos: 
- **FROM** para definir uma imagem;
- **RUN** para executar algum comando no processo de build da imagem;
- **CMD** para executar algum comando após a criação do container;
- **EXPOSE** para documentar qual porta deve ser liberada na criação do container;
- **COPY** e **ADD** para copiar arquivos locais e remotos para o container;
- **VOLUME** para definir um local onde serão armazenados arquivos que serão compartilhados com o host;
- **WORKDIR** para definir um ponto de partida de onde os arquivos serão executados;
- **USER** para definir qual usuário irá executar os comandos no container.





