# 📖 glossário de comandos Git

este glossário serve como um guia rápido de comandos Git para controle de versão.

---
## sumário

- [configuração inicial](#configuração-inicial)
- [inicialização e status](#inicialização-e-status)
- [adicionando e removendo do stage](#adicionando-e-removendo-do-stage)
- [commits e histórico](#commits-e-histórico)
- [trabalhando com branches](#trabalhando-com-branches)
- [repositório remoto](#repositório-remoto)


## configuração inicial 

```bash
$ git config --global user.name "seu nome"
# define o nome do usuário globalmente (omita --global para definir apenas no repositório atual)

$ git config --global user.email "email@git.com"
# define o e-mail do usuário globalmente

$ git config --list
# exibe todas as variáveis configuradas

$ git branch -m <name>
# altera o nome da branch atual

$ git config --global color.ui auto
# ativa o uso de cores nas saídas do terminal para melhor visualização 

$ git config --global core.editor vim gedit
# define o editor de texto padrão

$ git config --global core.autocrlf input
# windows e linux identificam o fim da linha de um arquivo de formas diferentes
# ao definir como input, ambos os sistemas identificam de forma igual
# assim, os diffs, merges e commits são idênticos em ambos os sistemas

$ git config --global alias.st status
# um alias é uma espécie de atalho de texto que otimiza o workflow
# aqui, ele substitui `$ git status` por `$ git st`

$ ssh-keygen
# gera um par de chaves (pública e privada) para autenticação segura
```

## inicialização e status

```bash
git init .
# transforma a pasta atual em um repositório Git

git status
# verifica o estado dos arquivos (quais foram alterados ou estão no stage)
```

## adicionando e removendo do stage

```bash
git add arquivo.md
# adiciona um arquivo específico para o stage (preparação para o commit)

git add .
# adiciona todas as alterações da pasta atual ao stage

git add --all
# adiciona todas as alterações de todo o repositório

git add *.md
# adiciona todos os arquivos com extensão .txt

git add comandos_*
# adiciona todos os arquivos que comecem com "comandos_"

git restore --staged arquivo.md
# remove o arquivo do stage (desfaz o 'git add')
```

>[!TIP]
> o símbolo `*` é um ***wildcard (curinga).*** ***wildcards***  auxiliam na manipulação de arquivos.  
> `*` seleciona *todos*.  
> `?` seleciona apenas *um*.  
> `[]` busca o *intervalo* informado. é diferente de *brace expansion* `{}`, que **gera** ao invés de buscar.  
>> exemplo: `$ cat ~/quotes/*.txt > ~/quotes/all-quotes.txt` lê todos os arquivos .txt da pasta e os adiciona a um único arquivo.

## commits e histórico

```bash
$ git commit -m "descrição da alteração"
# envia as alterações que estão no stage com uma mensagem explicativa

$ git log
# exibe o histórico de todos os commits realizados

$ git diff
# exibe as diferenças entre o arquivo commitado e a alteração atual

$ git diff --staged
# exibe as mudanças no stage que ainda não foram commitadas

$ git commit --amend -m "nova mensagem corrigida"
# corrige mensagem do commit anterior
# sempre usar antes do `git push`
```

## trabalhando com branches

```bash
git branch
# lista as branches existentes e indica em qual você está

git branch -M main
# define o nome da branch atual como 'main' de forma forçada (-M)  

git checkout -b nova_branch
# cria uma nova branch e já alterna para ela

git checkout nome_da_branch
# alterna para uma branch já existente

git merge outra_branch
# mescla o conteúdo da branch especificada para dentro da branch em que você está
```

## repositório remoto

```bash
git remote -v
# lista os endereços dos repositórios remotos vinculados

git push -u origin main
# envia os commits locais para o repositório remoto
# '-u' vincula o repo remoto e o local, permitindo usar apenas 'git push' em commits futuros na branch local 'main'
```