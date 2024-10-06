# Comandos Docker

Essa aula apresentou alguns comandos básicos do Docker, que são essenciais para gerenciar containers.

## Índice

- [Listando Containers](#listando-containers)
- [Executando Containers](#executando-containers)
- [Outros Comandos](#outros-comandos)
- [Exemplos](#exemplos)
- [Comandos Docker: Uma Visão Geral](#comandos-docker-uma-visão-geral)
- [Dicas](#dicas)
- [Próximos Passos](#próximos-passos)

## Listando Containers

- `docker ps`: Lista os containers em execução.
- `docker container ls`: Equivalente ao `docker ps`, mas mais semântico.
- `docker ps -a`: Lista todos os containers, incluindo os que foram encerrados.
- `docker container ls -a`: Equivalente ao `docker ps -a`, mas mais semântico.

## Executando Containers

- `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`: Cria e executa um container a partir de uma imagem.

## Outros Comandos

- `docker run --help`: Mostra as opções disponíveis para o comando `docker run`.

## Exemplos

- `docker run ubuntu`: Cria e executa um container a partir da imagem `ubuntu`. O container irá executar o comando `bash` por padrão.
- `docker run ubuntu sleep 1d`: Cria e executa um container a partir da imagem `ubuntu`, executando o comando `sleep 1d`. O container irá permanecer em execução por um dia.

Lembre-se que esses são apenas alguns dos comandos básicos do Docker. Existem muitos outros comandos disponíveis, que você pode explorar à medida que avança no curso.

---

## Comandos Docker: Uma Visão Geral

Essa aula explorou alguns comandos essenciais para gerenciar containers Docker. Aqui está um resumo dos comandos e suas funções:

### Gerenciando Containers

- `docker ps`: Lista os containers em execução.
- `docker ps -a`: Lista todos os containers, incluindo os que foram encerrados.
- `docker run [image]`: Cria e inicia um novo container a partir de uma imagem.
- `docker stop [container_id]`: Interrompe a execução de um container.
- `docker start [container_id]`: Reinicia um container que foi interrompido.
- `docker restart [container_id]`: Reinicia um container, mesmo que ele esteja em execução.
- `docker pause [container_id]`: Pausa a execução de um container.
- `docker unpause [container_id]`: Despausa a execução de um container.
- `docker rm [container_id]`: Remove um container.

### Interagindo com Containers

- `docker exec -it [container_id] [command]`: Executa um comando dentro de um container em modo interativo.
- `docker exec [container_id] [command]`: Executa um comando dentro de um container sem interação.

### Outras Funções

- `docker images`: Lista as imagens Docker disponíveis no sistema.
- `docker pull [image]`: Baixa uma imagem Docker do repositório.
- `docker push [image]`: Envia uma imagem Docker para o repositório.

---

## Dicas

- Use `-t=0` com `docker stop` para interromper um container instantaneamente.
- Utilize `docker exec -it` para acessar o terminal de um container em execução.
- Lembre-se que os containers são efêmeros, então os dados não são persistidos a menos que você configure uma solução de persistência.

## Próximos Passos

- Explore os comandos em mais detalhes e pratique sua utilização.
- Investigue as opções de persistência de dados para containers.
- Comece a construir seus próprios containers Docker.

Lembre-se: A prática é fundamental para dominar o Docker. Experimente os comandos e explore as diversas funcionalidades que ele oferece!

---

## Comandos Docker da Aula

Essa aula explorou os seguintes comandos do Docker:

### Gerenciando Containers

- `docker run`: Cria e inicia um novo container.
  - `-d`: Executa o container em segundo plano (detached).
  - `-P`: Mapeia aleatoriamente portas do container para portas do host.
  - `-p <porta_host>:<porta_container>`: Mapeia uma porta específica do host para uma porta específica do container.
- `docker ps`: Lista os containers em execução.
- `docker port <container_id>`: Mostra o mapeamento de portas do container.
- `docker rm <container_id>`: Remove um container.
  - `--force`: Força a remoção do container, mesmo que esteja em execução.

### Outros Comandos

- `docker hub`: Plataforma online para encontrar e compartilhar imagens Docker.

### Exemplo de Uso

```bash
# Iniciar um container em segundo plano com mapeamento de portas aleatório
docker run -d -P dockersamples/static-site

# Listar os containers em execução
docker ps

# Verificar o mapeamento de portas do container
docker port <container_id>

# Remover um container
docker rm <container_id> --force
```

--- 

<!---
Conteúdo extra

Título: "Comandos do Docker para gerenciar imagens e containers"
Seções:
Visualizando imagens:
docker images ou docker image ls: Lista todas as imagens baixadas no sistema.
Exemplo: docker images
Inspecionando imagens:
docker inspect <IMAGE_ID>: Exibe informações detalhadas sobre uma imagem, incluindo camadas, tags, data de criação, etc.
Exemplo: docker inspect f589ccde7957
Visualizando o histórico de uma imagem:
docker history <IMAGE_ID>: Mostra o histórico de uma imagem, incluindo as camadas e as instruções que foram usadas para criá-la.
Exemplo: docker history f589ccde7957
Criando um container a partir de uma imagem:
docker run <IMAGE_NAME> <COMMAND>: Cria um container a partir de uma imagem e executa um comando dentro dele.
Exemplo: docker run -it ubuntu bash
Outras informações:
Explique o conceito de camadas de uma imagem e como elas são reutilizadas para criar containers.
Descreva a diferença entre imagens e containers.
Mencione a importância da otimização de imagens para melhorar o desempenho dos containers.

---

Criando sua primeira imagem Docker
Essa aula te guiará na criação da sua primeira imagem Docker, utilizando uma aplicação Node como exemplo.

Pré-requisitos
Docker instalado e configurado em sua máquina.
Conhecimento básico sobre o funcionamento do Docker.
Editor de texto de sua preferência (ex: Visual Studio Code).
Criando o arquivo Dockerfile
Crie um novo arquivo chamado Dockerfile na raiz do seu projeto.
Defina a imagem base:
css
Copiar código
FROM node:14
Essa linha indica que você usará a imagem oficial do Node na versão 14 como base para sua imagem.
Defina o diretório de trabalho:
bash
Copiar código
WORKDIR /app-node
Essa linha define /app-node como o diretório de trabalho padrão dentro do container.
Copie os arquivos do seu projeto para o container:
sql
Copiar código
COPY . .
Essa linha copia todos os arquivos do seu diretório atual (onde está o Dockerfile) para o diretório /app-node dentro do container.
Instale as dependências do seu projeto:
undefined
Copiar código
RUN npm install
Essa linha executa o comando npm install dentro do container para instalar as dependências do seu projeto.
Defina o ponto de entrada do container:
sql
Copiar código
ENTRYPOINT npm start
Essa linha define o comando npm start como o ponto de entrada do container. Quando o container for iniciado, esse comando será executado.
Criando a imagem
Abra o terminal e navegue até o diretório do seu projeto.
Execute o comando docker build para criar a imagem:
bash
Copiar código
docker build -t danielartini/app-node:1 .
-t danielartini/app-node:1 define o nome da imagem como danielartini/app-node e a tag como 1.
. indica que o Dockerfile está no diretório atual.
Iniciando um container
Execute o comando docker run para iniciar um container a partir da imagem criada:
bash
Copiar código
docker run -d -p 8081:3000 danielartini/app-node:1.0
-d inicia o container em modo detached.
-p 8081:3000 mapeia a porta 8081 do seu host para a porta 3000 do container.
danielartini/app-node:1.0 especifica a imagem e a tag a serem utilizadas.
Acessando a aplicação
Após iniciar o container, você poderá acessar sua aplicação no navegador através do endereço localhost:8081.

Próximos passos
Explore a documentação do Docker para aprender mais sobre as instruções do Dockerfile.
Experimente criar imagens para outros tipos de aplicações.
Utilize as instruções ENV, EXPOSE, VOLUME e LABEL para personalizar suas imagens.

---



-->