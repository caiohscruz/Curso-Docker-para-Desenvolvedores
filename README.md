# Curso-Docker-para-Desenvolvedores

[Link do curso](https://www.udemy.com/course/docker-para-desenvolvedores-com-docker-swarm-e-kubernetes/)

## Comandos

- Containers
  - docker run <image>: cria um container segundo uma imagem, exista ela localmente ou não (consultar [hub.docker](https://hub.docker.com/))
    - flag -d : detached - mantem container rodando em background
    - flag -it: interative - mantem container rodando no console
    - flag -p x:y: seta porta para comunicação, sendo x a porta externa e y a porta do container
    - flag --name: para dar um nome personalizado para um container
  - docker start <id/name>: roda container criado previamente
  - docker stop <id/name>: para a execução de um container
  - docker rm <id/name>: exclui um container
    - flag -f: força a exclusão, caso o container esteja em execução
- Imagens
  - docker build <path>: cria uma imagem, path é onde o Dockerfile se encontra
  - docker image ls: para listar as imagens
  
