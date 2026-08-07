# 📓 Docker | anotações

esse documento contém anotações sobre containers e Docker, com o objetivo de facilitar a absorção dos conceitos. 

---

## sumário

- [o que é um container?](#o-que-é-um-container)
  - [container vs máquina virtual](#container-vs-máquina-virtual)
- [Docker](#docker)
  - [Dockerfile, Docker images e Docker containers](#dockerfile-docker-images-e-docker-containers)
  - [camadas de imagem](#camadas-de-imagem)
    - [por que isso importa?](#por-que-isso-importa)
    - [mecanismos de filesystem](#mecanismos-de-filesystem)
  - [instruções](#instruções)

## o que é um container?

- um container é um **grupo de processos** executados de **forma isolada**
- o **isolamento** acontece por um **mecanismo do kernel** do Linux chamado de *namespaces*
- a funcionalidade *namespaces* **restringe os recursos** que esse grupo de processos pode **acessar/visualizar**
- por conta dessa restrição, é possível criar **ambientes isolados**, conhecidos como **containers**
- em outras palavras: faz com que um container **enxergue somente a si mesmo**

> [!NOTE]
> o *namespaces* cria uma **visão isolada** de **cada um** dos recursos abaixo e, dessa forma, um container/processo possui uma **visão única** dos recursos globais do sistema, **diferente** da real e da dos demais containers:
> 
> - **PID** - ID do processo
> - **USER** - processo de usuário e grupo
> - **UTS** - *hostname* e nome de domínio
> - **MNT** - *mount point* (ponto de montagem)
> - **NET** - dispositivos de rede, pilhas de protocolo e portas
> - **IPC** - *inter-process communication*: permite troca de dados e sincronização entre processos  
> 
> esses são os principais, existem outros.

- **cgroups** *(grupos de controle)* é o mecanismo que controla, limita e monitora o uso dos recursos do sistema pelos containers
- portanto, containers são compostos por *namespaces* e *cgroups*, que possibilitam o **isolamento em relação a outros containers e ao dispositivo (*host*)**

### container vs máquina virtual

- cada instância de uma VM possui um sistema operacional próprio e completo
- um grupo de containers compartilha o **mesmo kernel/OS**, diferentemente das VMs, e por isso são **mais leves** e **mais rápidos** para inicializar 
- containers possibilitam **melhor aproveitamento de recursos**
- é possível utilizar **mais containers do que VMs** em um mesmo dispositivo

## Docker

- Docker é uma plataforma feita para ajudar na criação, uso e compartilhamento de containers
- as ferramentas que possibilitam a criação de **containers já existiam** e, apesar de úteis, **não eram tão acessíveis**
- Docker surgiu para **simplificar** o seu uso e torná-las **acessíveis** para as massas

### Dockerfile, Docker images e Docker containers

- Dockerfile é o **conjunto de instruções** que definem como a imagem será criada
- Docker image é o resultado da **construção (*build*)** dessas instruções
- o container em si é o resultado da **execução** da imagem

>[!TIP]
>  utilizando uma analogia, o Dockerfile pode ser pensado como a **receita** de um bolo; a imagem representa o **bolo pronto**, que é o resultado da aplicação da receita; e o container é o **bolo servido**, o resultado final das etapas anteriores.

### camadas de imagem

- uma camada é gerada por uma **instrução/comando** dentro do Dockerfile. algumas camadas incrementam o **tamanho da imagem**, outras são apenas camadas de **metadados** e não afetam o armazenamento  
- camadas são ***read-only (R/O)*** e, sendo assim, **imutáveis**. a ***camada de escrita (R/W)***, entretanto, é **mutável** e reside no topo  
- camadas são como blocos de construção, a mais recente é posicionada acima da anterior, e são divididas em categorias:  
		- **camada base:** `FROM` ─ é a base do sistema, como uma distro Linux (Alpine, Ubuntu)  
		- **camadas de imagem:** `RUN`, `COPY`, `ADD` ─ modificam o sistema de arquivos
		- **camadas de metadados:** `CMD`, `ENV`, `EXPOSE`, `LABEL` ─ não modificam arquivos, mas definem configurações. são camadas intermediárias  
		- **camada do container:** ao executar o container, o Docker adiciona a camada de escrita (a fina e temporária camada do topo) e **todo arquivo modificado, criado ou deletado existe apenas nessa camada**, preservando o estado das anteriores  

#### por que isso importa?

- camadas semelhantes podem ser **compartilhadas** entre imagens, pois ficam **salvas em cache**
- ou seja, diferentes imagens podem **reaproveitar camadas**, desde que sua ordem seja idêntica
- ao criar uma nova imagem, o Docker checa as camadas em cache **sequencialmente** e, se a **sequência de camadas for semelhante**, ele as **reutiliza** ao invés de refazê-las
- porém, se uma das camadas/instruções for **diferente**, todas as seguintes são **invalidadas** e devem ser **refeitas do zero**

>[!IMPORTANT]
>saber disso é importante, pois permite **otimizar imagens**, que é o ato de **deixar as instruções que mudam frequentemente sempre no final** do Dockerfile e, assim, obter benefícios como:  
>- armazenamento eficaz: ao ter **sequências de camadas iguais**, diferentes imagens irão utilizar os **mesmos arquivos associados**, ao invés de criar novos  
>- economia de infraestrutura: ao utilizar a **mesma imagem em centenas ou milhares de containers**, apenas as diferentes **camadas de escrita vão fazer diferença no seu armazenamento**   
>- execução mais rápida: se o Docker **já executou uma imagem**, essa execução está **salva em cache** e rodar imagens otimizadas garante que a **mesma execução seja compartilhada por diferentes imagens**  
>
> ter esses pontos em mente, em ambiente de produção, pode **otimizar e acelerar pipelines CI/CD** e **economizar custos em infraestrutura**, seja em nuvem ou *on-premises*

#### mecanismos de filesystem  

- **Union File System (UnionFS)**: é o conceito de empilhar e **unificar** diferentes camadas em um **único sistema de arquivos**, ou seja, as transforma em uma visão só 
- **Copy-on-Write (CoW)**: regra que faz com que os arquivos que necessitam de **modificação**, mas que pertencem às camadas R/O sejam **copiados** para a camada de escrita e modificados nela, **preservando** o estado dos arquivos originais
- **Whiteout**: como as camadas R/O **não podem ser modificadas** durante a execução, o Docker cria um **arquivo de marcação** na camada de escrita, responsável por **ocultar os arquivos**, criando a ilusão de que foram deletados 
- **overlay2:** é o *driver* do Docker que de fato aplica o conceito de *UnionFS* e as regras *CoW (copiar pro topo e então escrever)* e *Whiteout (ocultar o que foi deletado)*

### instruções

- `FROM` ─ é a camada base, as demais camadas são construídas a partir dela. é uma boa prática usar uma tag específica ao invés de *latest*, para garantir que as dependências não mudarão no futuro e que a otimização não seja quebrada se o Docker digest da imagem mudar  
- `RUN` ─ executa comandos necessários pra imagem, como instalar programas ou pacotes, mudar permissões ou editar arquivos. comandos `RUN` são executados no momento da construção *(build)*
- `CMD` ─ se usado mais de uma vez, o **mais recente sobrescreve** os anteriores. é executado ao iniciar o container
- `COPY` ─ copia arquivos para uma nova camada de imagem. por ser uma camada que costuma mudar frequentemente, é uma boa prática deixá-la **próximo ao final** do Dockerfile, visando otimizar a imagem

> [documentação oficial do Docker sobre todos os comandos possíveis ](https://docs.docker.com/reference/dockerfile)