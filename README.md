# Curso-Docker-para-Desenvolvedores

[Link do curso](https://www.udemy.com/course/docker-para-desenvolvedores-com-docker-swarm-e-kubernetes/)

## Comandos

- Containers
  - `docker run <image>` = cria um container segundo uma imagem, exista ela localmente ou não (consultar [hub.docker](https://hub.docker.com/))
    - flag `-d` = detached - mantem container rodando em background
    - flag `-it` = interative - mantem container rodando no console
    - flag `-p x:y` = seta porta para comunicação, sendo x a porta externa e y a porta do container
    - flag `--name` = para dar um nome personalizado para um container
  - `docker start <container>` = roda container criado previamente
  - `docker stop <container>` = para a execução de um container
  - `docker ps` =  consulta os container em execução
    - flag `-a` = inclui no resultado também os containers parados
  - `docker rm <container>` = exclui um container
    - flag `-f` = força a exclusão, caso o container esteja em execução
  - `docker cp <name>:<path_in> <path_out>` = copia um arquivo de dentro de um container para fora
  - `docker top <container>` = consulta os processos rodando no container
  - `docker inspect <container>` = inspeciona informações como id, data de criação, imagem e muito mais
- Imagens
  - `docker build <path>` = cria uma imagem, path é onde o Dockerfile se encontra
  - `docker image` = para listar as imagens
  - `docker rmi <image>` = exclui uma imagem
- Geral
  - `docker system prune` = remove tudo quanto é imagem, container ou network não utilizado
  - `docker status` = consulta quantos recursos estão sendo alocados para os containers
