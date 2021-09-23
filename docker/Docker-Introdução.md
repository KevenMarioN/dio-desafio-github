# Docker - Introdução

Created: September 3, 2021 12:35 PM
Professor: Luis Miguel Flores dos Santos
Property: Médio

# Conceitos

## Tipos de estruturas

1. Uma unica aplicação rodando em um Hardware
2. Várias aplicações rodando no mesmo hardware usando mesmas bibliotecas, ou seja caso uma atualize pode ocorrer o derrubamento de outros serviços.
3. Um hardware com hypervisor, um sistema para cada aplicação. Atualizando sem afetar a aplicação que está rodando juntamente.
4. Servidor fisico com Container Engine, compartilha mesma imagem de sistema operacional.

## [MeuApp.com](http://meuapp.com) →

1. Proxy/Serviço → Escalonamento Horizontal
    1. Fazendo a distribuição dos clientes que acessam.
    2. Fazendo um "Balanceamento de Carga".
2. Fácil Atualização 
    1. Updates 
        1. Criando Novo Container
        2. Verifica se as portas estão correspondendo
        3. Mata o docker antigo, caso o update for bem sucedido
    2. Docker Swarm | Kubernetes | Docker Compose

# Terminologias

1. Container image
    1. Pacote com todas as dependências da aplicação
2. DockerFile
    1. Instruções para criar o doker
3. Build
    1. Gera a imagem apartir do dockerfile
4. Container
    1. Imagem gera pelo build colocada em ação
5. Volumes
    1. Aplicação cair os dados fica salvo
6. Tag
    1. Versionamentos das imagens
7. Multi-stage Build
8. Repository
    1. Caixa cheia de imagens
9. Registry
    1. Serviço que prove acesso ao repository
10. Docker Hub
    1. Imagens → Repository
11. Compose
    1. Multiplos container

## Como Funciona ?

Docker_Client

- Docker build → Dockerfile → Docker run
- Docker pull → Puxa do Docker Hub para o local → Docker run
- Docker run → executa os dockers

Docker_Host

- Docker daemon → Registry
- Images | Criadas ou do Docker Hub
    - Containers
        - Container → Aplicação

Registry 

- Docker Hub

## Prática → [https://labs.play-with-docker.com/](https://labs.play-with-docker.com/)

$ docker run 

--name {first-container} → nome do container

-p {8080} → porta utilizada pelo container

-d {nginx} → Imagem que vai ser puxada da Docker Hub

### Remover Docker

docker rm {names} → se o container estiver parada

docker rm -f {names} → se o container estiver ativo durante a remoção

### Ver imagens disponiveís

docker images

### Remover Images

docker rmi {nome da image}

Aws

Azure

## Principais Comandos

1. Run → Criar Container
2. Ps → Lista container
3. Info → Informações do Docker
4. Images → Imagens para criar containers
5. Exec → Executar binários
6. Stop, Start
7. Logs → Lista outputs do container
8. Inspect → Lista todas as config do container
9. Pull → puxa do Docker Hub uma imagem
10. Commit →Comiar modificações no container
11. Tag → nomeia, melhora versionamento
12. Login, Logout
13. Push → subir uma imagem para docker hub
14. Search → procurar uma imagem
15. Rm → remover container
16. Rmi → remove a imagem
17. Export, import →Container
18. Save , Load → save imagem do docker

## Intro

$ docker run 

--name {first-container} → nome do container

-p {8080} → porta utilizada pelo container

-d {nginx} → Imagem que vai ser puxada da Docker Hub

sleep 3600 → tempo que o docker vai ficar aberto

## Interno

docker exec 

site → nome do container

mkdir → comando

## Acessar  Container

docker exec → executar no container x

-it 

{hello} → Nome do container

sh → Acessar pelo ssh

## Após configuração do docker, e possível executar comandos no container

## Cria uma imagem personalizada

docker commit

—author="{Nome aqui dentro}"

—message="Mensagem"

{container}

{nome da imagem}

## Personalizar images

docker tag

{images name}

"nome:versao"

## Tipos de Rede

- Bridge → Default, utilizado para comunicação entre containers
- Host → Remove isolamento, o container responde diretamente pela placa de rede do host
- Overlay → Permite comunicação entre containers de hosts diferentes.
- Macvlan → Permite atribuir um endereço MAC → disponibilizando visível ao dispositivo físico na rede.
- none → Sem rede

## Criar rede

docker network → executar as funcões de rede

 create -d → criação

 bridge  → tipo de network criada

petsBridge → nome de indentificação

para usar a brigde, ao criar o container add flag —net {nome da conexão}

## Criando um cluster

$ docker swarm 

init 

--advertise-addr 

192.168.0.28 {ip da maquina}

Após ser gerado o cluster, e abrir as portas necessárias. um código será gerado.

$ docker network create -d overlay petsOverlay

## Criando serviços

docker service create 

--network petsOverlay 

--name db 

consul → image

## Escalona

docker service

scale

web=3

# Armazenamento no docker

## Tipos de armazenamento

- Volume
    - Docker engine tem total autonomia
    - Torna mais pesado a execução
    - Criado quando criar o container
- Bind Mounts
    - mapea um arquivo no host e compartilha no container
    - informações permanentes
- tmpfs mount → memoria temporaria
    - disco para uso temporario
    - cache
    - logs não necessários

docker volume create {meuPrimeiroVolume}

## Criando Volume

$ docker volume create meuPrimeiroVolume

$ docker run -d -p 80:80 --name container-volume --mount source=meuPrimeiroVolume,target=/usr/share/nginx nginx

Mesmo removendo o Container, os dados permanecem.

## Criando tmpfs

docker run -d --name container-tmpfs 

--mount type=tmpfs,destination=/cache,tmpfs-size=100000

 busybox sleep 3600

## Projeto no ar

1. Limite
    1. Podemos limitar utilização de : 
        1. Memoria → 
            1. —memory {10m} → 10 megas de RAM
        2. CPU
            1. —cpus=".5"

## Executar dockerfile

docker-compose up -d
