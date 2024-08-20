# Instalação do Docker

O Docker pode ser instalado em diferentes sistemas operacionais, sendo as principais plataformas suportadas o Linux e o Windows. A seguir, apresentamos um guia detalhado para instalação em cada uma dessas plataformas, além de uma alternativa para usuários de Windows que preferem um ambiente mais semelhante ao Linux.

## Instalação no Linux

A instalação do Docker no Linux pode variar um pouco dependendo da distribuição que você está usando. Abaixo, fornecemos instruções para as distribuições mais comuns: Ubuntu, Debian e CentOS.

### Ubuntu

1.  **Atualize o sistema:**

    ```
    sudo apt-get update
    sudo apt-get upgrade
    ```

2.  **Instale pacotes de pré-requisitos:**

    ```
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
    ```

3.  **Adicione a chave GPG oficial do Docker:**

    ```
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

4.  **Adicione o repositório do Docker ao APT sources:**

    ```
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

5.  **Atualize o APT e instale o Docker:**

    ```
    sudo apt-get update
    sudo apt-get install docker-ce
    ```

6.  **Verifique se a instalação foi bem-sucedida:**

    ```
    sudo systemctl status docker
    ```

7.  **(Opcional) Execute Docker sem sudo:**

    ```
    sudo usermod -aG docker ${USER}
    ```

Saia e entre novamente na sessão para aplicar as mudanças.

## Instalação no Windows

### Docker Desktop

A instalação do Docker no Windows é feita através do Docker Desktop, que é uma aplicação que fornece uma experiência de desenvolvimento Docker fácil de usar no Windows. Siga os passos abaixo para instalar o Docker Desktop:

1.  **Baixe o Docker Desktop:**
    1. Acesse o site oficial do Docker Desktop em [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2.  **Instale o Docker Desktop:**
    1.  Execute o instalador e siga as instruções na tela. Certifique-se de marcar a opção para instalar o Docker e o WSL 2, se necessário.
3.  **Verifique a instalação:**
    1.  Abra o Windows PowerShell e execute: `docker --version`, isso deve retornar a versão do Docker instalada.

### WSL 2

O WSL 2 (Windows Subsystem for Linux 2) permite que você execute uma distribuição Linux nativamente no Windows 10 e 11, oferecendo uma maneira de usar Docker em um ambiente Linux diretamente no Windows.

1.  **Ative o WSL:**
    1. Abra o Windows PowerShell como administrador e execute: `wsl --install`. Isso irá habilitar o WSL e instalar a distribuição padrão do Linux. Pode ser necessário reiniciar o computador.
2.  **Configure o WSL 2 como padrão:**
    1. Após a reinicialização, defina o WSL 2 como a versão padrão: `wsl --set-default-version 2`
3.  **Instale uma distribuição Linux:**
    1.  Baixe e instale a distribuição de sua escolha (como Ubuntu) na Microsoft Store.
4.  **Instale o Docker no WSL**:
    1.  Dentro da distribuição Linux (ex: Ubuntu), siga as instruções de instalação do Docker para Linux fornecidas anteriormente.
5.  **Integrar com o Docker Desktop (Opcional):**
    1.  Docker Desktop pode ser integrado ao WSL 2 para fornecer uma experiência híbrida, onde o Docker Desktop gerencia os containers através do WSL 2. Nas configurações do Docker Desktop, ative a integração com o WSL 2. Isso permite que você execute comandos Docker tanto no Windows quanto no Linux.

## Conclusão

Após seguir as etapas de instalação correspondentes ao seu sistema operacional, você estará pronto para começar a trabalhar com Docker. Se você estiver no Windows e preferir um ambiente Linux, o WSL 2 é uma excelente alternativa, proporcionando a flexibilidade de usar comandos Linux com o Docker diretamente no seu sistema Windows.
