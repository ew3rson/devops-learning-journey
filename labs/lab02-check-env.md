# 🤫 lab 02 — validação silenciosa de ambiente

este laboratório demonstra a prática de manipulação dos fluxos de saída (`stdout` e `stderr`) para gerar scripts silenciosos.

---

```bash
#!/usr/bin/env bash

command -v git &> /dev/null && echo "Git pronto para uso!" || echo "Git não instalado."
```

---

## **aprendizados**

- `command -v` permite verificar se um programa está instalado e retorna seu caminho.

- os redirecionadores dos *file descriptors*: 
    - `>` redireciona o `stdout`
    - `2>` redireciona o `stderr`
    - `&>` redireciona ambos

- o `&> /dev/null` é usado para descartar mensagens do sistema, é o que permite o script trabalhar de forma silenciosa. também conhecido como *buraco negro*.

- o operador `&&` serve como um condicional curto: ele só executa o comando a seguir caso o anterior retorne **0 (sucesso)**.

- o operador `||`, diferente do anterior, executa o comando a seguir se o atual retornar um **exit code diferente de 0**. 