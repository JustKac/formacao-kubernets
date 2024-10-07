# Comandos Docker

## Índice

- [Listando Containers](#listando-containers)
- [Executando Containers](#executando-containers)
- [Outros Comandos](#outros-comandos)
- [Exemplos](#exemplos)
- [Comandos Docker: Uma Visão Geral](#comandos-docker-uma-visão-geral)
- [Dicas](#dicas)
- [Próximos Passos](#próximos-passos)
- [Comandos do Docker para gerenciar imagens e containers](#comandos-do-docker-para-gerenciar-imagens-e-containers)

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

## Comandos do Docker para gerenciar imagens e containers

### Visualizando Imagens

- `docker images` ou `docker image ls`: Lista todas as imagens baixadas no sistema.
  - Exemplo: `docker images`

### Inspecionando Imagens

- `docker inspect <IMAGE_ID>`: Exibe informações detalhadas sobre uma imagem, incluindo camadas, tags, data de criação, etc.
  - Exemplo: `docker inspect f589ccde7957`

### Visualizando o Histórico de uma Imagem

- `docker history <IMAGE_ID>`: Mostra o histórico de uma imagem, incluindo as camadas e as instruções que foram usadas para criá-la.
  - Exemplo: `docker history f589ccde7957`

### Criando um Container a partir de uma Imagem

- `docker run <IMAGE_NAME> <COMMAND>`: Cria um container a partir de uma imagem e executa um comando dentro dele.
  - Exemplo: `docker run -it ubuntu bash`