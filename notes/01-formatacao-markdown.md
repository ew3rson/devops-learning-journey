# ✒️ formatação de documentos em linguagem Markdown

este documento é um guia rápido de utilização da linguagem de marcação Markdown.

a linguagem Markdown é muito utilizada em documentação técnica e também para formatar arquivos README, com foco em legibilidade e organização do documento.

---

## hierarquia de títulos

```md
# título do documento (normalmente usa-se # apenas uma vez)
## seção
### subseção
```

## listas

```md
- item de lista
	- subitem
- outro item

1. primeiro item
2. segundo item
```

## destaque de texto

```md
**negrito**
*itálico*
`inline code`
```

## bloco de código

```bash
ls -R
git status
```
```python
print('hello, world')
```

## exemplo de arquivo

```md
# título do arquivo 
descrição do arquivo. ex.: esse documento contém X com o objetivo de Y

## seção 1 
**texto em negrito**
- item 1
- item 2
- [ ] checkbox
  
### subseção 1
deve-se seguir a hierarquia: subseção vem após uma seção

### subseção 2
texto

## seção 2  
1. primeiro passo
2. segundo passo 
   
[link clicável](https://www.github.com)   

> blockquote
> [!NOTE] bloco para nota
> [!TIP] bloco para dica
> [!WARNING] bloco para aviso
> [!CAUTION] bloco para cautela

--- linha horizontal
```
