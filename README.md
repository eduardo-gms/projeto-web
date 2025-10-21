# Exercício: Criação de um Ambiente de Desenvolvimento Full-Stack com Docker Compose

## Cenário

Você foi encarregado(a) de criar um ambiente de desenvolvimento padronizado e reprodutível para uma nova aplicação web. O objetivo é garantir que toda a equipe de desenvolvimento possa trabalhar em um ambiente idêntico, simplificando a configuração inicial e evitando problemas de "na minha máquina funciona".

## Objetivo Principal

Desenvolver uma configuração com `docker-compose.yml` que orquestre um ecossistema de serviços para uma aplicação web moderna, incluindo frontend, backend, banco de dados, uma ferramenta de administração de banco de dados e um proxy reverso.

## Requisitos Técnicos

Você deve criar a estrutura de arquivos e as configurações necessárias para atender aos seguintes requisitos:

1.  **Configuração Centralizada:** Todas as variáveis configuráveis (portas, credenciais de usuário, senhas e nomes de banco de dados) devem ser definidas em um arquivo `.env` na raiz do projeto.

2.  **Serviço de Frontend:**
    * Deve ser baseado na imagem `node:lts-alpine`.
    * Projetado para uma aplicação **React com Vite**.
    * Deve suportar **hot-reloading** para refletir alterações no código-fonte em tempo real.
    * Um `Dockerfile` customizado deve ser criado para este serviço.

3.  **Serviço de Backend:**
    * Deve ser baseado na imagem `node:lts-alpine`.
    * Projetado para uma aplicação **NestJS**.
    * Deve suportar **hot-reloading** para o desenvolvimento.
    * Um `Dockerfile` customizado deve ser criado para este serviço.

4.  **Serviço de Banco de Dados:**
    * Utilizar a imagem oficial `postgres:alpine`.
    * Os dados devem ser **persistentes**, sobrevivendo à recriação do container, através do uso de um volume Docker.

5.  **Serviço de Admin do Banco de Dados:**
    * Utilizar a imagem `dpage/pgadmin4`.
    * As credenciais de login devem ser configuráveis via variáveis de ambiente.
    * As configurações (ex: servidores salvos) devem ser persistentes.

6.  **Serviço de Proxy Reverso:**
    * Utilizar a imagem `nginx:alpine`.
    * Deve ser configurado através de um `Dockerfile` e um arquivo `nginx.conf` customizado.
    * **Regras de Roteamento:**
        * Requisições para a rota raiz (`/`) devem ser direcionadas ao serviço de **frontend**.
        * Requisições para o caminho `/api/` (e seus sub-caminhos) devem ser direcionadas ao serviço de **backend**, e o prefixo `/api` deve ser removido antes do encaminhamento.

7.  **Rede:**
    * Todos os serviços devem se comunicar em uma única rede bridge customizada, definida no `docker-compose.yml`.

## Entregáveis

* Uma estrutura de diretórios contendo todos os arquivos de configuração necessários para levantar o ambiente (`docker-compose.yml`, todos os `Dockerfile`s, `nginx.conf`, e um `.env.example` com as chaves das variáveis).

## Critérios de Avaliação

* O ambiente completo deve ser iniciado com um único comando: `docker-compose up --build`.
* As alterações de código nos diretórios locais do frontend e backend devem ser refletidas nos containers em execução sem a necessidade de um novo build.
* Todos os serviços devem estar acessíveis em suas respectivas portas mapeadas no host.
* As regras de roteamento do Nginx devem funcionar conforme especificado.
* Os dados do PostgreSQL e do pgAdmin devem ser mantidos após a execução do comando `docker-compose down` e `docker-compose up`.