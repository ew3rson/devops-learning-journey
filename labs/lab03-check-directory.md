# 📂 lab 03 — validação de diretório e navegação

script para validar a existência de um diretório e gerenciar a navegação no terminal, garantindo que o comando `cd` afete a sessão atual do usuário através do uso do comando `source`.

---

```bash
#!/usr/bin/env bash
# digite 'source lab03_diretorio.sh' para iniciar o script

GREEN="\e[32m"
RED="\e[31m"
RESET="\e[0m"
DIR="estudos_bash"

validar() {
	if [ -d "$DIR" ]; then # a flag -d indica que está testando um diretório
	    echo -e "Acessando o diretório ${GREEN}${DIR}${RESET}..."
	    cd "$DIR" || { echo -e "${RED}Erro ao acessar diretório.${RESET}"; return 1; } 
	    pwd
	    return 0
	else 
    echo -e "${RED}Erro! Diretório não encontrado.${RESET}"
    return 1
	fi
}

validar
# use o comando 'echo $?' após rodar o script para visualizar o exit code
```

---

## **aprendizados**

- **bloco condicional**: o `[` (comando `test`) é usado para avaliar a expressão e retornar um `exit code` (0 para verdadeiro, diferente de 0 para falso). isso permite controlar o fluxo do script com `if`.
	- sem isso, o script **tentará abrir** o diretório. em condicionais que já retornam um `exit code` ele não é necessário.

- **`exit code` e `return code`**: `return` dá erro se não for usado em uma função ou com `source`. já o `exit` encerra o script e retorna o código de saída especificado.

- **ShellCheck**: utilizei a ferramenta ShellCheck para analisar o script e identificar possíveis erros ou más práticas em Bash.

## desafios / erros encontrados

- caso utilize `exit` ao invés de `return`, o script irá rodar isoladamente (em um *subshell*), e a troca de diretório só ocorrerá enquanto o script estiver rodando.

- para a troca de diretório funcionar na sessão atual, é preciso usar o comando `source` ao iniciar o script.

- porém, usar `exit` ao invés de `return` em modo `source` faz com que o terminal feche sozinho. isso ocorre porque o `source` faz o terminal executar os comandos na sessão atual (no processo que está aberto).

- testei o cenário de `Erro ao acessar diretório.` ao remover a permissão de execução da pasta `estudos_bash` e rodar o script.
