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
  - `docker kill $(docker ps -q)` = para a execução de todos os containers
  - `docker rm $(docker ps -a -q)` = para a execução de todos os containers e os remove
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
- Compose
  - `docker-compose up` = executa o compose
  - `docker-compose down` = derruba os containers
  - `docker-compose ps` = lista containers gerenciados pelo compose
    - flag `-d` = detached - mantem container rodando em background
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

  Setup Docker Swarm na AWS
  - `sudo yum update -y` = atualiza a máquina
  - `sudo yum install docker` = instala docker
  - `sudo service docker start` = inicializa docker
  - `sudo usermod -a -G docker ec2-user` = vincula usuário
  - `sudo docker swarm init` =  inicia swarm
    - tag `--advertise-addr <IP>` =  caso solicite por IP
  - `sudo docker swarm leave` = interrompe swarm
    - tag `-f` = caso dê erro relacionado com Manager

  Docker Swarm
  - `docker node ls` = lista os nodes com seus status
  - `docker node rm <id>` = remove node do swarm
  - `docker swarm join --token <TOKEN> <IP>:<PORTA>` = adiciona worker
  - `sudo docker swarm join-token manager` = recupera o token

  Services
  - `docker service create --name <name> <image>` = subindo serviço
    - `--replicas <number>` = para incluir réplicas
    - `--network <name>` = para setar uma rede
  - `docker service ls` = lista serviços
  - `docker service rm <name>` = lista serviços
  - `docker service inspect <id>` = inspeciona serviço
  - `docker service ps <id>` = confere container rodando o serviço serviço
  - `docker node update --availability drain <id>` = faz com que o serviço não receba mais ordens do manager
  - `docker node update --availability active <id>` = faz com que o serviço volte a receber ordens do manager
  - `docker service update --image <image> <service>` = atualiza imagem dos nodes com status active referentes a um dado serviço
  - `docker service update --network-add <network> <service>` = para setar uma rede para um serviço já criado

  - `docker network create --drive overlay <name>` = o tipo de rede para nodes do swarm é overlay

  Compose com Swarm
  - `docker stack deploy -c <file.yaml> <name>` = cria um serviço via compose
  - `docker service scale <name>=<number>` = replica o serviço para number máquinas

  Dica para terminal
  - `Crtl + Shift + C` ou `Crtl + Insert` em vez de `Crtl + C`
  - `Crtl + Shift + V` ou `Shift + Insert`em vez de `Crtl + V`

