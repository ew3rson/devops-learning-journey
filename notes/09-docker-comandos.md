# 🐋 comandos Docker

este documento é um glossário de comandos Docker e é complementar às [anotações sobre Docker](/notes/08-docker.md).

```bash
$ docker run <nome-imagem>
# executa o container baseado na imagem definida

$ docker run --detach <nome-imagem>
# a flag -d executa o container em segundo plano

$ docker run -d --name <novo-nome> <nome-imagem>
# a flag --name personaliza o nome do container
# se um nome não for definido, o Docker gerará um aleatório

$ docker run --publish 8080:80 <nome-imagem>
# a flag -p expõe a porta definida 

$ docker pull <nome-imagem>
# faz o download da imagem, mas o container não é executado

$ docker ps
# exibe informações dos containers em execução no momento
# a flag '-a' permite obter informações de containers já executados

$ docker exec -it <id>
# permite executar comandos dentro do container

$ docker containter stop <id>
# encerra o container

$ docker stop $(docker ps -aq)
# encerra todos os containers existentes

$ docker rm <nome-container>
# deleta o container

$ docker rmi <nome-imagem>
# deleta imagem

$ docker rmi $(docker ps -aq)
# deleta todos as imagens existentes

$ docker system prune
# remove containers parados, volumes não usados, imagens não associadas a containers e cache

$ docker image prune
# remove apenas imagens não associadas a containers
```