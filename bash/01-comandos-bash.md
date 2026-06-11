# 📖 glossário de comandos Bash

este glossário serve como um guia rápido de comandos do interpretador Bash para consulta e referência durante os estudos.

---

## sumário  
  
1. [informações do usuário e ambiente](#informações-do-usuário-e-ambiente)  
2. [gerenciamento de processos](#gerenciamento-de-processos)  
3. [gerenciamento de usuários](#gerenciamento-de-usuários)  
4. [gerenciamento de permissões](#gerenciamento-de-permissões)  
5. [saída e exibição](#saída-e-exibição)  
6. [listagem e navegação](#listagem-e-navegação)  
7. [gerenciamento de arquivos e diretórios](#gerenciamento-de-arquivos-e-diretórios)  
8. [gerenciamento de armazenamento](#gerenciamento-de-armazenamento)
9. [compactar e extrair arquivos](#compactar-e-extrair-arquivos)
10. [Secure Shell (SSH)](#secure-shell-ssh)
11. [edição de texto](#edição-de-texto)

## informações do usuário e ambiente

```bash
$ whoami			
# exibe o nome do usuário atual

$ pwd 
# exibe o caminho absoluto do diretório atual 

$ echo ~			
# exibe o caminho do diretório home (~ representa o home)

$ echo $0
# exibe o nome do shell em uso

$ file <arquivo>
# exibe informações do arquivo
# 'ELF' se refere a um arquivo binário
# 'data' se refere a um arquivo cujo tipo não pôde ser identificado
```

>[!TIP]
>`$ curl cheat.sh/comando` permite ver informações práticas sobre o **comando** inserido.  
> muito útil como alternativa prática ao `$ man`.

## gerenciamento de processos

```bash
$ top
# exibe informações sobre o sistema e processos
# similar ao gerenciador de tarefas do windows
# a tecla 'd' permite alterar o tempo de atualização da exibição

$ pstree
# exibe os processos em formato de árvore

$ pgrep -f <pid>
# pesquisa processo pelo pid
# não retorna nada se o processo não estiver ativo
```

## gerenciamento de usuários

```bash
$ sudo useradd <nome>
# cria novo usuário

$ sudo userdel <nome>
# deleta o usuário, mas mantém sua home 

$ sudo userdel -r <nome>
# remove o usuário e sua home

$ sudo useradd -m joker
# além do novo usuário, cria o diretório home automaticamente

$ sudo useradd -m -d /home/arkham joker
# permite definir o nome e diretório da home do usuário antes de criá-lo

$ sudo usermod -d /home/belle-reve joker
# modifica a home do usuário

$ sudo usermod -s /bin/bash joker
# alterna o shell padrão do usuário

$ sudo usermod -aG sudo joker
# adiciona usuário a um grupo (neste caso, sudo)

$ ls -ld /home/arkham
# checa se o diretório home existe

$ sudo grep -w 'joker' /etc/passwd
# exibe informações sobre o usuário (útil para checar se ele foi criado)

$ sudo grep -E '^(joker|batman):' /etc/passwd
# exibe informações de mais de um usuário ao mesmo tempo

$ sudo passwd joker
# define/altera a senha do usuário

$ sudo passwd -S joker
# checa o status da senha do usuário

$ sudo passwd -l joker
# bloqueia a conta do usuário

$ sudo passwd -u joker
# desbloqueia a conta do usuário

$ su - joker
# troca de usuário (su: switch user)
```

## gerenciamento de permissões

```bash
$ sudo chown <owner:group> arquivo.md
# altera o proprietário e grupo de um arquivo ou diretório

$ chmod 000 arquivo.md
# altera as permissões de um arquivo ou diretório
# os zeros representam: owner, group, others
# as permissões são organizadas em binário: 4 (read); 2 (write); 1 (execute); 0 (no permission)

$ chmod -R 700 ~/newdir
# altera recursivamente as permissões do diretório
# boa prática ao lidar com diretórios

$ chmod -R u+rwx ~/newdir
# equivalente em symbolic notation do comando anterior
# u (owner/user); g (group); o (others)
# r (read); w (write); x (execute)

$ chmod -R a+rwx ~/newdir
# a = all
# concede permissão a todos
```

>[!TIP]
> o gerenciamento das permissões com **números** é chamado de ***numeric notation***.  
> a forma mais intuitiva, que utiliza **letras** e **operadores**, é chamada de ***symbolic notation***. 

## saída e exibição

```bash
$ echo 'texto'
# exibe o texto digitado (útil para mensagens em scripts e automação)

$ cat file.md
# visualiza o conteúdo de um arquivo diretamente no terminal

$ cat -n arquivo.md
# -n é uma flag/option
# ela enumera as linhas do documento
# útil em arquivos com várias linhas

$ head arquivo.md
# head permite ver as primeiras 10 linhas de um arquivo

$ head -n1 arquivo.md
O
# ao usar a flag -n e o número 1, é possivel ver apenas a primeira linha
# o número define a quantidade de linhas a ser exibida. ex.: -n2, -n3

$ head -c2 file.md
Oi
# o -c2 faz head exibir apenas o primeiro byte/caractere do texto
# o número define a quantidade de caracteres a ser exibida

$ tail -n1 file.md
# tail é o oposto de head, exibe a última linha

$ tail -c1
# com a flag -c, ele não costuma exibir nada se o parâmetro for 1

$ diff file1 file2
1c1
< hello file1
---
> hello file2
# 1c1 indica que a linha 1 do arquivo 1 é diferente da primeira linha do segundo

$ diff -r ~/Desktop ~/Code
# -r faz diff comparar recursivamente os diretórios e exibir os arquivos que constam em apenas um deles

$ file <arquivo>
# exibe informações adicionais sobre o arquivo
```

## listagem e navegação

```bash
$ ls
# lista arquivos e diretórios da pasta atual

$ ls -l
# exibe informações detalhadas com permissões e proprietário 

$ ls -a
# lista todos os arquivos, incluindo os ocultos

$ ls -la
# une os dois acima: lista tudo com detalhes

$ ls -ld
# exibe informações detalhadas do diretório somente

$ ls -R
# lista o conteúdo do diretório e de todos os seus subdiretórios

$ ls -lR
# lista detalhada e recursiva

$ cd
# navega entre diretórios, significa change directory
# o comando sozinho leva para a home do usuário 

$ cd ~
# atalho para a home

$ cd .
# referência à pasta atual

$ cd ..
# sobe um nível na hierarquia (vai para a pasta mãe)

$ du -sh ~/
# exibe o espaço usado pelo diretório
# sh = summary + human readable
```

## gerenciamento de arquivos e diretórios

```bash
$ touch arquivo.txt
# cria um novo arquivo vazio

$ touch file{1..20}.txt
# atalho para criar múltiplos arquivos de uma vez (ex: file1 até file20)
# é chamado brace expansion

$ mkdir pasta
# cria novo diretório

$ mkdir -p pasta/subpasta
# cria a pasta e a subpasta automaticamente
# sem isso, a tentativa de criar subpasta gera erro

$ cp arquivo.txt copia.txt
# copia um arquivo

$ cp -r pasta/ copia_pasta/
# copia um diretório de forma recursiva (incluindo tudo o que há dentro)

$ mv arquivo.txt novo_nome.txt
# renomeia um arquivo ou diretório

$ mv arquivo.txt pasta/
# move o arquivo para dentro de um diretório

$ mv testdir/name.txt ./newname.txt
# move o arquivo para fora de uma pasta já renomeando-o

$ rm arquivo.txt
# remove um arquivo

$ rm -i arquivo.txt
# solicita confirmação antes de excluir (mais seguro)

$ rm -rf pasta/
# remove de forma recursiva e forçada (apaga tudo sem perguntar)
# USAR COM CAUTELA

$ rmdir pasta_vazia
# remove um diretório, mas apenas se ele estiver vazio

$ ln -s <path> <atalho>
# cria symbolic link de um diretório 

$ wget <link>
# faz o download do arquivo do link

$ wget -O <path> <link>
# realiza o download no caminho (output) especificado 

$ curl <url>
# transfere o conteúdo da página/servidor para o terminal e permite interagir com sua API 
```

## gerenciamento de armazenamento

```bash
$ df -h ~
# exibe informações do armazenamento
# -h torna as informações human-readable

$ du -h ~
# exibe as informações de forma detalhada por diretório

$ free -m
# exibe informações da memória
```

## compactar e extrair arquivos

```bash
$ tar czf <arquivo.tar.gz> <arquivo>
# --create --gzip --file 
# cria e compacta arquivo e especifica o nome

$ tar --create --xz --file <arquivo>
# define extensão .xz ao invés de .gz

$ tar --create --xz --file <arquivo> --directory ~/.local
# define o diretório do arquivo a ser extraído 

$ tar --extract --file --xz <arquivo.xz>
# `tar xf <arquivo.xz` também funciona

$ tar xzf <arquivo.tar.gz>
# --extract --gzip --file
# extrai arquivo

$ unzip <arquivo.zip>
# descompacta arquivo
# funciona apenas com arquivos .zip

$ tar --list --files <arquivo.tar>
# lista conteúdo do arquivo compactado
```

## Secure Shell (SSH)

```bash
$ sudo systemctl enable --now sshd
# ativa o daemon do ssh (sshd)
# systemctl controla serviços do sistema
# a flag --now torna a mudança imediata

$ systemctl is-active sshd
# verifica se o daemon foi ativado

$ systemctl status sshd
# exibe informações detalhadas do daemon

$ ssh username@hostname
# permite se conectar a um dispositivo remoto
# o @ define a conexão
# o username define o nome de usuário a ser exibido
# hostname costuma ser o endereço IP do dispositivo

$ scp ~/Documents/arquivo.md username@hostname:~/Documents
# copia o arquivo para o dispositivo remoto
# é possível fazer o contrário invertendo a ordem dos argumentos

$ ssh-keygen -t ed25519
# gera um par de chaves SSH (SSH key pair), uma é privada e outra pública 
# a flag -t é usada para definir o algoritmo da criptografia (ed25519)

$ ssh-copy-id username@hostname
# copia a chave SSH pública para o dispositivo remoto
```

## edição de texto

```bash
$ nano arquivo.txt
# abre o editor de texto nano para criar ou editar arquivos
# CTRL + O: salva as alterações
# CTRL + X: sai do editor

$ vim arquivo.txt
# abre o editor de texto vim para criar ou editar arquivos
# 'i' e 'a': permite escrever texto
# 'esc': permite digitar comandos 
# ':w': salva as alterações (write)
# ':q: sai do editor (quit)
# é possível combinar comandos, como ':wq'
```