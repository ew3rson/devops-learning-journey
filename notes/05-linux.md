# 📓 Linux | anotações

estas anotações são registros sobre o sistema operacional GNU/Linux para entendimento e fixação de seus aspectos principais.

---

## fundamentos

- o GNU/Linux é totalmente regido pelo princípio de **código livre/aberto**.
- surgiu como consequência do movimento software livre (**Free Software Movement**) fundado por **Richard Stallman**.
- o **objetivo** do movimento era criar um **sistema Unix-like**, disponível **livremente para todos**.
- o sistema operacional em si foi idealizado pelo **Projeto GNU**, que significa **GNU is Not Unix** — também fundado por **Richard Stallman**.

- Linux **não** é de fato o **sistema operacional**, mas sim o *kernel* do **GNU OS**.
- um *kernel* é o núcleo de um sistema, a **interface que conecta** o hardware e o software de um computador.
- o Linux surgiu como a **peça que faltava** para o **Projeto GNU** — o real **OS** que consiste em vários **pacotes** — mas que ainda não possuía um *kernel* devido a alta complexidade no seu desenvolvimento.
- hoje é **conhecido popularmente** apenas por **Linux**, sem o GNU, apesar de seu nome oficial ser **GNU/Linux**.

## aspectos

- o Linux é disposto em uma **árvore hierárquica**, com o diretório `/` sendo o seu **principal** — toda hierarquia do sistema se **origina dele**.
- no Linux, **tudo é considerado um arquivo**, incluindo pastas e **até mesmo o hardware**: a interação do *mouse* com o sistema, por exemplo, é representada por um **arquivo de texto** que é constantemente **incrementado** pelo movimento do dispositivo.
> [!IMPORTANT]
> é possível **manipular** quase tudo do sistema através da linha de comando **justamente** porque o Linux **abstrai** o hardware e as configurações em **arquivos**. 
- é extremamente seguro, pois segue o conceito de **privilégio mínimo** — um usuário comum **não** pode realizar alterações críticas no sistema, apenas o **superusuário (root)** pode, através do comando `sudo` **(substitute user/superuser do)**.
- o Linux não identifica o **tipo** de um arquivo pela sua **extensão**, ao invés disso, o sistema verifica o conteúdo do arquivo e/ou seu **cabeçalho (header)** — conhecidos como *magic numbers* — e os **compara** com uma lista de tipos conhecidos pelo sistema, se um arquivo não possui um **tipo conhecido** pelo sistema, ele recebe o tipo `data`.
> [!TIP]
> o banco de dados dos tipos conhecidos — conhecido como **Magic Database** — é encontrado em `/usr/share/file/magic.mgc`.  
> para tornar o conteúdo de um binário *human-readable* usa-se o comando `strings`.
> `$ strings /usr/share/file/magic.mgc`.

## diretórios importantes

- `/etc` — possui arquivos de configuração
- `/tmp` — armazena arquivos temporários e os remove após 30 dias
- `/usr` — contém comandos e aplicações
- `/var` — armazena arquivos que variam de tamanho durante a execução do sistema.