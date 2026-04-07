# 👥 lab 04 — gestão de usuários e permissões

esse laboratório registra a sequência de comandos para criar um grupo de usuários que compartilham o mesmo ambiente de trabalho no Linux, aplicando o conceito de **privilégio mínimo.**

> **cenário**: criar um diretório de trabalho onde apenas membros do grupo `batfamily` tenham controle sobre os arquivos.

---

## comandos

1. **criar** novo grupo:

```bash
$ sudo groupadd batfamily
```

2. **verificar** se o grupo foi criado:

```bash
$ getent group batfamily
batfamily:x:1004:
```

3. **criar** usuários e **adicioná-los** ao grupo:

```bash
# a flag -m cria a home e a flag -g permite definir o grupo
$ sudo useradd -m -g batfamily batman
$ sudo useradd -m -g batfamily robin
$ sudo useradd -m -g batfamily batgirl
```

4. **exibir** informações do usuário:

```bash
$ id robin
uid=1005(robin) gid=1004(batfamily) groups=1004(batfamily)
```


5. **definir** senha para os usuários:
```bash
# sudo passwd username
$ sudo passwd batman
```

6. **verificar** se a senha do usuário está definida:

```bash
# 'P' significa que a senha está definida
$ sudo passwd -S batman
batman P 2026-03-16 0 99999 7 -1
# se um 'L' aparecer no lugar, indica que a conta está bloqueada
```

7. **criar** o diretório de trabalho e **definir** o grupo dono:

```bash
# cria o diretório
$ sudo sudo mkdir /srv/missions

# define o grupo como proprietário
$ sudo chown :batfamily /srv/missions
```

8. **definir** as permissões do grupo:

```bash
# permissões de leitura, escrita e execução para o 'owner' e o 'group'
$ sudo chmod 775 /srv/missions
# permissões de leitura e execução para o 'others'
```

9. **exibir** as permissões do diretório:

```bash
$ ls -ld /srv/missions
drwxrwxr-x 2 root batfamily 4096 Mar 15 21:55 /srv/missions
# o 'd' no início indica que é um diretório
```

---

## aprendizados

- **pasta /srv:** essa pasta costuma ser a mais indicada para alocar diretórios de projetos compartilhados, se criar na `/home` haverá problemas de permissão. 

- **permissão de grupo:** ao definir um grupo como dono da pasta de trabalho, todos os usuários associados a ele podem colaborar no mesmo diretório.

- **numeric notation:** reforcei o entendimento do conceito de notação numérica para permissões; que são:
	- `7` **(owner)**: `4` (read), `2` (write), `1` (execute).
	- `7` **(group)**: `4` (read), `2` (write), `1` (execute).
	- `5` **(others)**: `4` (read), `0` (write), `1` (execute).