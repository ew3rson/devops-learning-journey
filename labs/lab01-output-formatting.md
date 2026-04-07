# 🎨 lab 01 — formatação de saída CLI

demonstração do uso de variáveis e códigos ANSI para formatar a saída de textos no terminal para melhor legibilidade.

---

```bash
#!/usr/bin/env bash

GREEN="\033[32m"
YELLOW="\033[33m"
RED="\033[31m"
RESET="\033[0m"

echo -e "${RED}Universidade Presbiteriana Mackenzie${RESET}\nCurso: ${GREEN}Análise e Desenvolvimento de Sistemas"
```

---

## **aprendizados**

- como declarar variáveis em Bash.  

- definir cores em um script para melhorar sua legibilidade.

- a flag `-e` no comando `echo` é o que permite interpretar códigos ANSI, como as quebras de linha (`\n`) e as cores.
	- `printf` é uma alternativa, e costuma ser mais consistente para essa finalidade.

