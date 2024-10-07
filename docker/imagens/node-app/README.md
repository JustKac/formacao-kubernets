# Criando sua Primeira Imagem Docker

Essa aula te guiará na criação da sua primeira imagem Docker, utilizando uma aplicação Node como exemplo.

## Índice

- [Pré-requisitos](#pré-requisitos)
- [Criando o Arquivo Dockerfile](#criando-o-arquivo-dockerfile)
- [Criando a Imagem](#criando-a-imagem)
- [Iniciando um Container](#iniciando-um-container)
- [Acessando a Aplicação](#acessando-a-aplicação)
- [Incrementando a Imagem](#incrementando-a-imagem)
- [Lendo Variáveis de Ambiente](#lendo-variáveis-de-ambiente)
- [Exemplos de Uso](#exemplos-de-uso)
- [Publicando no Docker Hub](#publicando-no-docker-hub)
- [Conclusão](#conclusão)
- [Dicas](#dicas)

## Pré-requisitos

- Docker instalado e configurado em sua máquina.
- Conhecimento básico sobre o funcionamento do Docker.
- Editor de texto de sua preferência (ex: Visual Studio Code).

## Criando o Arquivo Dockerfile

1. Crie um novo arquivo chamado `Dockerfile` na raiz do seu projeto.
2. Defina a imagem base:
    ```dockerfile
    FROM node:14
    ```
    Essa linha indica que você usará a imagem oficial do Node na versão 14 como base para sua imagem.
3. Defina o diretório de trabalho:
    ```dockerfile
    WORKDIR /app-node
    ```
    Essa linha define `/app-node` como o diretório de trabalho padrão dentro do container.
4. Copie os arquivos do seu projeto para o container:
    ```dockerfile
    COPY . .
    ```
    Essa linha copia todos os arquivos do seu diretório atual (onde está o Dockerfile) para o diretório `/app-node` dentro do container.
5. Instale as dependências do seu projeto:
    ```dockerfile
    RUN npm install
    ```
    Essa linha executa o comando `npm install` dentro do container para instalar as dependências do seu projeto.
6. Defina o ponto de entrada do container:
    ```dockerfile
    ENTRYPOINT ["npm", "start"]
    ```
    Essa linha define o comando `npm start` como o ponto de entrada do container. Quando o container for iniciado, esse comando será executado.

## Criando a Imagem

1. Abra o terminal e navegue até o diretório do seu projeto.
2. Execute o comando `docker build` para criar a imagem:

    ```bash
    docker build -t danielartini/app-node:1 .
    ```
    - `-t danielartini/app-node:1` define o nome da imagem como `danielartini/app-node` e a tag como [`1`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fcaioh%2Fcode%2Fpessoal%2Fgithub-justkac%2Fformacao-kubernets%2Fdocker%2Fimagens%2Fnode-app%2FREADME.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A39%2C%22character%22%3A38%7D%7D%5D%2C%22fa46787a-05ff-4938-88c8-0abbe791611a%22%5D "Go to definition").
    - `.` indica que o Dockerfile está no diretório atual.

## Iniciando um Container

Execute o comando `docker run` para iniciar um container a partir da imagem criada:
```bash
docker run -d -p 8081:3000 danielartini/app-node:1.0
```
- `-d` inicia o container em modo detached.
- `-p 8081:3000` mapeia a porta 8081 do seu host para a porta 3000 do container.
- `danielartini/app-node:1.0` especifica a imagem e a tag a serem utilizadas.

## Acessando a Aplicação

Após iniciar o container, você poderá acessar sua aplicação no navegador através do endereço `localhost:8081`.

## Incrementando a Imagem

### Documentando a Porta com EXPOSE

Objetivo: Informar a porta em que a aplicação dentro do container está executando, facilitando o mapeamento de portas e o uso da imagem por outras pessoas.

Comando: `EXPOSE <porta>`

Exemplo:
```dockerfile
FROM node:14
WORKDIR /app-node
EXPOSE 3000
COPY . .
RUN npm install
ENTRYPOINT ["npm", "start"]
```
Observação: O comando [`EXPOSE`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fcaioh%2Fcode%2Fpessoal%2Fgithub-justkac%2Fformacao-kubernets%2Fdocker%2Fimagens%2Fnode-app%2FREADME.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A54%2C%22character%22%3A140%7D%7D%5D%2C%22fa46787a-05ff-4938-88c8-0abbe791611a%22%5D "Go to definition") apenas documenta a porta, não a expõe automaticamente. Para expor a porta, você precisa usar o comando `docker run -p` ou `docker run -P`.

## Lendo Variáveis de Ambiente

Objetivo: Tornar a imagem mais parametrizável, permitindo que a porta da aplicação seja definida no momento da criação do container.

Comandos:
- `ARG <nome_da_variavel>=<valor_padrao>`: Define uma variável de ambiente em tempo de build.
- `ENV <nome_da_variavel>=<valor>`: Define uma variável de ambiente dentro do container.

Exemplo:
```dockerfile
FROM node:14
WORKDIR /app-node
ARG PORT_BUILD=3000
ENV PORT=$PORT_BUILD
EXPOSE $PORT_BUILD
COPY . .
RUN npm install
ENTRYPOINT ["npm", "start"]
```
Observação:
- O [`ARG`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fcaioh%2Fcode%2Fpessoal%2Fgithub-justkac%2Fformacao-kubernets%2Fdocker%2Fimagens%2Fnode-app%2FREADME.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A82%2C%22character%22%3A0%7D%7D%5D%2C%22fa46787a-05ff-4938-88c8-0abbe791611a%22%5D "Go to definition") é usado apenas em tempo de build da imagem.
- O [`ENV`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fcaioh%2Fcode%2Fpessoal%2Fgithub-justkac%2Fformacao-kubernets%2Fdocker%2Fimagens%2Fnode-app%2FREADME.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A83%2C%22character%22%3A0%7D%7D%5D%2C%22fa46787a-05ff-4938-88c8-0abbe791611a%22%5D "Go to definition") é usado dentro do container, após a imagem ser criada.
- A variável [`PORT_BUILD`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fcaioh%2Fcode%2Fpessoal%2Fgithub-justkac%2Fformacao-kubernets%2Fdocker%2Fimagens%2Fnode-app%2FREADME.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A97%2C%22character%22%3A4%7D%7D%5D%2C%22fa46787a-05ff-4938-88c8-0abbe791611a%22%5D "Go to definition") definida com [`ARG`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fcaioh%2Fcode%2Fpessoal%2Fgithub-justkac%2Fformacao-kubernets%2Fdocker%2Fimagens%2Fnode-app%2FREADME.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A82%2C%22character%22%3A0%7D%7D%5D%2C%22fa46787a-05ff-4938-88c8-0abbe791611a%22%5D "Go to definition") é usada para definir a variável [`PORT`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fcaioh%2Fcode%2Fpessoal%2Fgithub-justkac%2Fformacao-kubernets%2Fdocker%2Fimagens%2Fnode-app%2FREADME.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A98%2C%22character%22%3A4%7D%7D%5D%2C%22fa46787a-05ff-4938-88c8-0abbe791611a%22%5D "Go to definition") com [`ENV`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fcaioh%2Fcode%2Fpessoal%2Fgithub-justkac%2Fformacao-kubernets%2Fdocker%2Fimagens%2Fnode-app%2FREADME.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A83%2C%22character%22%3A0%7D%7D%5D%2C%22fa46787a-05ff-4938-88c8-0abbe791611a%22%5D "Go to definition").

## Exemplos de Uso

- Parar todos os containers em execução:
    ```bash
    docker stop $(docker container ls -q)
    ```
- Criar um container com a imagem `caiolins/app-node:1.1` e expor a porta 3000:
    ```bash
    docker run -d caiolins/app-node:1.1
    ```
- Criar um container com a imagem `caiolins/app-node:1.2` e definir a porta 6000:
    ```bash
    docker run -d caiolins/app-node:1.2
    ```
- Criar um container com a imagem `caiolins/app-node:1.2` e mapear a porta 9090 da máquina para a porta 6000 do container:
    ```bash
    docker run -p 9090:6000 -d caiolins/app-node:1.2
    ```

## Publicando no Docker Hub

1. Crie uma conta gratuita no [Docker Hub](https://hub.docker.com/).
2. Certifique-se de ter o Docker instalado em sua máquina.

### Passos

1. Autenticando no Docker Hub:
    ```bash
    docker login -u <seu_usuario>
    ```
    Explicação: Este comando autentica sua conta no Docker Hub. Você será solicitado a inserir sua senha.
2. Criando uma tag para a imagem:
    ```bash
    docker tag <imagem_original>:<tag_original> <seu_usuario>/<nome_da_imagem>:<tag_nova>
    ```
    Explicação: Este comando cria uma nova tag para sua imagem, usando seu nome de usuário do Docker Hub.
3. Subindo a imagem para o Docker Hub:
    ```bash
    docker push <seu_usuario>/<nome_da_imagem>:<tag_nova>
    ```
    Explicação: Este comando envia a imagem para o Docker Hub.

### Exemplos

- Subindo a imagem `danielartini/app-node:1.0` para o Docker Hub:
    ```bash
    docker tag danielartini/app-node:1.0 aluradocker/app-node:1.0
    docker push aluradocker/app-node:1.0
    ```
- Subindo a imagem `danielartini/app-node:1.2` para o Docker Hub:
    ```bash
    docker tag danielartini/app-node:1.2 aluradocker/app-node:1.2
    docker push aluradocker/app-node:1.2
    ```