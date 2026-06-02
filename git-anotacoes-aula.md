# 🍒 Cherry-pick e Blame — Anotações de Aula

> Comandos para compartilhar commits entre branches e rastrear mudanças

---

## 🌿 Criando e navegando entre branches

```bash
git branch                        # lista todas as branches existentes
git switch -c nome-da-branch      # cria e já entra na nova branch
git switch main                   # volta para a branch main
git switch nome-da-branch         # entra em uma branch existente
```

---

## 📝 Salvando alterações (o fluxo normal)

```bash
git status                        # verifica o estado dos arquivos
git add nome-do-arquivo           # adiciona arquivo para o commit
git commit -m "mensagem"          # salva o commit
```

---

## 🍒 Cherry-pick — Pegando um commit de outra branch

**Quando usar:** duas funcionalidades precisam da mesma alteração, mas estão em branches separadas. Em vez de reescrever o código, você "copia" o commit de uma branch para outra.

```bash
# 1. Ver os commits de outra branch para achar o hash
git log nome-da-branch2

# 2. Estando na branch onde quer aplicar:
git cherry-pick <hash-do-commit>
```

> Exemplo visual:
> ```
> branch2:  A --- B(alteração) --- C
> branch1:  A --- B'  ← cópia do commit B aplicada aqui!
> ```

---

## 📤 Enviando branches para o GitHub

```bash
git push origin branch1 branch2   # envia duas branches de uma vez
```

---

## 🔀 Mergeando tudo na main

```bash
git switch main                   # volta para a main
git merge branch2                 # traz os commits da branch2
git merge branch1                 # traz os commits da branch1
git push origin main              # envia tudo para o GitHub
```

---

## 🔍 Git Blame — Descobrindo quem alterou cada linha

**Quando usar:** quer entender um trecho de código e saber com quem falar, ou quer saber quando uma linha foi adicionada.

```bash
git blame nome-do-arquivo
```

A saída mostra, **linha por linha**:

```
<hash>   (<Autor>   <data>  <hora>  <nº linha>)  <conteúdo>

609bc79b (Vinicius  2023-12-23 15:27  14) <title>
^250c665 (Rodrigo   2023-09-05 14:59   1) <!DOCTYPE html>
```

> 💡 O `^` indica o **primeiro commit** do projeto.

Para ver os detalhes completos de um commit encontrado:

```bash
git show <hash>
```

---

## 📋 Resumo rápido

| Comando | Para que serve |
|---------|----------------|
| `git branch` | Listar branches |
| `git switch -c nome` | Criar e entrar em nova branch |
| `git switch nome` | Entrar em branch existente |
| `git log nome-da-branch` | Ver commits de outra branch |
| `git cherry-pick <hash>` | Copiar commit de outra branch para a atual |
| `git push origin b1 b2` | Enviar duas branches ao GitHub |
| `git merge nome` | Trazer commits de uma branch para a atual |
| `git blame arquivo` | Ver quem alterou cada linha do arquivo |
| `git show <hash>` | Ver detalhes de um commit específico |

---

*Notas de aula — Curso Git & GitHub: Dominando Controle de Versão de Código (Alura)*
