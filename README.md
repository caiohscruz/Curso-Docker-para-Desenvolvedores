# Curso-Docker-para-Desenvolvedores

[Link do curso](https://www.udemy.com/course/docker-para-desenvolvedores-com-docker-swarm-e-kubernetes/)

## Comandos

- Containers
  - `docker run <image>` = cria um container segundo uma imagem, exista ela localmente ou não (consultar [hub.docker](https://hub.docker.com/))
    - flag `-d` = detached - mantem container rodando em background
    - flag `-it` = interative - mantem container rodando no console
    - flag `-p x:y` = seta porta para comunicação, sendo x a porta externa e y a porta do container
    - flag `--name <name>` = para dar um nome personalizado para um container
    - flag `--rm` = remove o container após execução
    - flag `--network <network>` = indica network a utilizar
  - `docker start <container>` = roda container criado previamente
  - `docker stop <container>` = para a execução de um container
  - `docker ps` =  consulta os container em execução
    - flag `-a` = inclui no resultado também os containers parados
  - `docker cp <name>:<path_in> <path_out>` = copia um arquivo de dentro de um container para fora
  - `docker top <container>` = consulta os processos rodando no container
  - `docker exec -it <container> bash` = permite abrir terminal interativo de container em execução
- Imagens
  - `docker build <path>` = cria uma imagem, path é onde o Dockerfile se encontra
    - flag `-t <name>:<tag>` = para dar nome e tag (opcional) 
  - `docker rmi <image>` = exclui uma imagem
- Volumes
  - `docker run -v <volume_name>:/<dir_container>` = cria um volume nomeado ou utiliza um volume já existente, dir_container contado desde do "workdir" do Dockerfile
  - `docker run -v <dir_out>:/<dir_container>` = vincula um diretório externo como volume, dir_out é o caminho absoluto do diretório
    - flag `:ro` = cria volume somente leitura, flag vem colada logo atrás do identificador
  - `docker volume create <name>` = para criar volume sem ser na criação de um container
- Networks
  - `docker network create <name>` = remove tudo quanto é imagem, container ou network não utilizado
  - `docker network connect <rede> <container>` = conecta um conteiner a uma rede
  - `docker network disconnect <rede> <container>` = disconecta um conteiner de uma rede
  - `docker network inspect <rede>` = inspeciona uma rede
- Geral
  - `docker system prune` = remove tudo quanto é imagem, container ou network não utilizado
  - `docker status` = consulta quantos recursos estão sendo alocados para os containers
  - `docker login` = autentica com o hub docker
  - `docker logout` = desautentica com o hub docker
  - `docker push <repository>` = para subir uma imagem para o hub, o nome da imagem deve ser o mesmo do repositório
    - `repository:tag` = o versionamento é feito com a tag
  - `docker pull <repository>` = para clonar uma imagem do hub, o nome da imagem deve ser o mesmo do repositório
  - `docker (container/image/volume) ls` = lista elementos, Bind Mounts não são listados.
  - `docker (container/image/volume) inspect <name>` = inspeciona o elemento
  - `docker (container/image/volume) prune` = remove o que não está sendo utilizado
  - `docker (container/image/volume) rm <name>` = remove um elemento
    - flag `-f` = força a exclusão, caso o container esteja em execução
- Container com MySQL
  - flag `-e MYSQL_ALLOW_EMPTY_PASSWORD=True` no `docker run` = permite uso de senha vazia

  Exemplos:
  - `docker exec -it phpmessages_container bash`
  - `docker run -d -p 82:80 --name phpmessages_container -v phpvolume:/var/www/html/messages --rm phpmessages`
  - `docker build -t flaskapinetwork .`
  - `docker run -d -p 5000:5000 --name flask_api_container --network flasknetwork --rm flaskapinetwork`

  YAML
  - `null` ou `~` = representam o nulo
  - `True` ou `On` = representam verdadeiro
  - `False` ou `Off` = representam falso
  - string pode ser declarada com ou sem aspas
  - `[1, 2, 3]` ou  (`obj:` \n ` - item`) = formas de representar arrays 
  - `{a: 1, b: 2, c: 3}` ou  (`obj:` \n ` key: value`) = formas de representar dicionários/objetos 

