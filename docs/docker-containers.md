# Docker Containers

Os containers são a essência da tecnologia Docker. Eles encapsulam uma aplicação e suas dependências em um ambiente isolado e portátil. Ao contrário das máquinas virtuais, os containers compartilham o kernel do sistema operacional, o que os torna muito mais leves e rápidos.

## O que é um Container Docker?

Um container Docker é uma instância de uma imagem Docker em execução. Ele é criado a partir de uma imagem e inclui tudo o que é necessário para executar uma aplicação de maneira consistente em diferentes ambientes, como código, bibliotecas e configurações.

Containers são isolados, imutáveis e efêmeros. Isso significa que eles operam em ambientes isolados, não são modificados durante a execução, e podem ser facilmente destruídos e recriados.

## Principais Características dos Containers

- **Leveza:** Compartilham o kernel do sistema, ocupando menos recursos do que VMs.
- **Portabilidade:** Funcionam da mesma forma em qualquer ambiente que suporte Docker.
- **Isolamento:** Processos e recursos dos containers são isolados uns dos outros.

## Trabalhando com Containers Docker

### Listar Containers

Para visualizar todos os containers em execução:

```
docker ps
```

### Iniciar, Parar e Remover Containers

- **Iniciar um container existente:**

```
docker start <container_id>
```

- **Parar um container em execução:**

```
docker stop <container_id>
```

- **Remover um container:**

```
docker rm <container_id>
```

### Criar e Executar um Novo Container

Para criar e executar um novo container a partir de uma imagem, use:

```
docker run -d --name meu-container nginx
```

- **`d`: Executa o container em segundo plano (detached mode).**
- **`name`: Atribui um nome ao container.**

### Acessar um Container em Execução

- **Para abrir um terminal interativo em um 
container em execução:**

```
docker exec -it <container_id> /bin/sh
```

### Inspecionar Containers

- **Para obter informações detalhadas de um container:**

```
docker inspect <container_id>
```

### Expor Portas e Mapear Volumes

- **Expor portas para acessar a aplicação fora do container:**

```
docker run -d -p 8080:80 nginx
```
Neste exemplo, a porta 8080 do host é mapeada para a porta 80 do container.

- **Mapear volumes para persistência de dados:**

```
docker run -d -v /meus-dados:/dados nginx 
```

### Excluir Containers em Massa

- **Para remover todos os containers parados:**

```
docker container prune
```

### Conclusão

Containers são fundamentais no Docker, proporcionando uma maneira eficiente de empacotar, distribuir e executar aplicações em diferentes ambientes. Com os containers, é possível garantir consistência, portabilidade e isolamento para suas aplicações, independentemente do ambiente onde elas estejam sendo executadas.

Para mais detalhes sobre containers, consulte a [documentação oficial do Docker](https://docs.docker.com/get-started/overview/).
