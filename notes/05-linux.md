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

