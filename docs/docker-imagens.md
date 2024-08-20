# Docker Imagens

As imagens do Docker são um dos conceitos fundamentais no Docker. Elas fornecem o ambiente necessário para que os contêineres sejam executados. Uma imagem do Docker é uma versão empacotada e imutável de uma aplicação ou serviço, incluindo todas as suas dependências, bibliotecas, configurações e outros arquivos necessários para sua execução.

## O que é uma Imagem Docker?

Uma imagem Docker é um pacote leve, independente e executável que inclui tudo o que é necessário para rodar uma peça de software, incluindo o código, runtime, bibliotecas, variáveis de ambiente e arquivos de configuração.

Imagens são imutáveis, o que significa que, uma vez criadas, não podem ser alteradas. No entanto, é possível criar novas imagens a partir de outras imagens usando o conceito de "camadas".

## Camadas em Imagens Docker

As imagens Docker são compostas por várias camadas. Cada instrução em um Dockerfile (como `RUN`, `COPY`, ou `ADD`) cria uma nova camada na imagem. As camadas são empilhadas umas sobre as outras, e juntas, formam a imagem final.

- **Camada Base:** A primeira camada de uma imagem Docker é frequentemente uma distribuição de sistema operacional mínima, como Alpine ou Debian.
- **Camadas de Instruções:** Instruções subsequentes no Dockerfile, como a instalação de pacotes ou a configuração de ambiente, criam novas camadas.

O Docker utiliza um sistema de camadas em que cada camada é uma diferença em relação à camada anterior. Isso permite reutilizar camadas entre diferentes imagens, economizando espaço em disco e acelerando o processo de construção de imagens.

## Trabalhando com Imagens Docker

### Listar Imagens

Para listar todas as imagens disponíveis localmente no seu sistema Docker, use o seguinte comando:

```
docker images
```

### Procurar Imagens no Docker Hub

O [Docker Hub](https://hub.docker.com/) é um repositório público de imagens Docker. Você pode procurar imagens disponíveis no Docker Hub usando o comando `docker search`. Por exemplo, para procurar imagens relacionadas ao NGINX, você pode executar:

```
docker search nginx
```

### Baixar Imagens

Para baixar uma imagem do Docker Hub, use o comando `docker pull`. Por exemplo, para baixar a imagem oficial do NGINX, você pode executar:

```
docker pull nginx
```

### Criar uma Imagem

Você pode criar suas próprias imagens personalizadas usando um arquivo chamado Dockerfile. O Dockerfile é um arquivo de texto que contém uma lista de instruções para construir uma imagem.

Aqui está um exemplo de um Dockerfile que cria uma imagem para um aplicativo Django que foi utilizado no projeto de programação web:

```Dockerfile
FROM python:3.11.3-alpine3.18
LABEL maintainer="erickescap@gmail.com"

# Essa variável de ambiente é usada para controlar se o Python deve
# gravar arquivos de bytecode (.pyc) no disco. 1 = Não, 0 = Sim
ENV PYTHONDONTWRITEBYTECODE 1

# Define que a saída do Python será exibida imediatamente no console ou em
# outros dispositivos de saída, sem ser armazenada em buffer.
# Em resumo, você verá os outputs do Python em tempo real.
ENV PYTHONUNBUFFERED 1

# Copia a pasta "djangoapp" e "scripts" para dentro do container.
COPY djangoapp /djangoapp
COPY scripts /scripts

# Entra na pasta djangoapp no container
WORKDIR /djangoapp

# A porta 8000 estará disponível para conexões externas ao container
# É a porta que vamos usar para o Django.
EXPOSE 8000

# RUN executa comandos em um shell dentro do container para construir a imagem.
# O resultado da execução do comando é armazenado no sistema de arquivos da
# imagem como uma nova camada.
# Agrupar os comandos em um único RUN pode reduzir a quantidade de camadas da
# imagem e torná-la mais eficiente.
RUN python -m venv /venv && \
    /venv/bin/pip install --upgrade pip && \
    /venv/bin/pip install -r /djangoapp/requirements.txt && \
    mkdir -p /data/web/static /data/web/media && \
    chmod -R 755 /data/web/static /data/web/media && \
    chmod -R +x /scripts

# Adiciona a pasta scripts e venv/bin
# no $PATH do container.
ENV PATH="/scripts:/venv/bin:$PATH"

# Executa o arquivo scripts/commands.sh
CMD ["commands.sh"]
```

**Explicação das instruções:**

- `FROM`: Define a imagem base para o container. Neste caso, o Python 3.11 rodando em Alpine Linux, uma distribuição mínima e eficiente.
- `LABEL`: Adiciona metadados à imagem, como o e-mail do responsável.
- `ENV`: Define variáveis de ambiente para otimizar o comportamento do Python dentro do container.
- `COPY`: Copia os arquivos da aplicação e scripts para o container.
- `WORKDIR`: Define o diretório de trabalho onde os comandos serão executados.
- `EXPOSE`: Indica que o container vai usar a porta 8000 para comunicação.
- `RUN`: Executa uma série de comandos para configurar o ambiente Python e preparar o container para rodar a aplicação Django.
- `ENV PATH`: Atualiza o PATH para incluir scripts e o ambiente virtual Python.
- `CMD`: Define o comando padrão a ser executado quando o container é iniciado.

Para construir a imagem a partir do Dockerfile, use o comando `docker build`. Por exemplo, para construir a imagem a partir do Dockerfile acima, você pode executar:

```
docker build -t minha-imagem .
```

### Excluir Imagens

Para remover uma imagem do seu sistema, use o comando `docker rmi`. Por exemplo, para remover a imagem do NGINX, você pode executar:

```
docker rmi minha-imagem
```

### Limpar Imagens Não Utilizadas

Para limpar imagens não utilizadas no seu sistema, você pode usar o comando `docker image prune`. Isso removerá todas as imagens que não estão associadas a nenhum contêiner em execução.

```
docker image prune
```

Caso você queira remover todas as imagens do seu sistema, incluindo as que estão associadas a contêineres em execução, você pode usar o comando `docker image prune -a`.

```
docker image prune -a
```

### Tag de Imagens

Você pode adicionar tags às imagens para identificá-las de forma mais fácil. Para adicionar uma tag a uma imagem, use o comando `docker tag`. Por exemplo, para adicionar a tag `latest` à imagem do NGINX, você pode executar:

```
docker tag minha-imagem minha-imagem:latest
```

### Enviar Imagens para o Docker Hub

Se você deseja compartilhar suas imagens com outras pessoas, você pode enviá-las para o Docker Hub. Primeiro, você precisa fazer login no Docker Hub usando o comando `docker login`. Em seguida, você pode enviar a imagem para o Docker Hub usando o comando `docker push`. Por exemplo, para enviar a imagem do NGINX para o Docker Hub, você pode executar:

```
docker login
docker push minha-imagem:latest
```

## Conclusão

As imagens do Docker são essenciais para o funcionamento dos contêineres. Elas fornecem um ambiente isolado e independente para a execução de aplicações e serviços. Compreender como trabalhar com imagens Docker é fundamental para aproveitar ao máximo a tecnologia de contêineres e garantir que suas aplicações sejam executadas de forma consistente e confiável em qualquer ambiente.

Para saber mais sobre imagens Docker, consulte a [documentação oficial do Docker](https://docs.docker.com/get-started/overview/).
