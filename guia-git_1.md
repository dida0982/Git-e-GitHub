# 📋 Guia Prático de Comandos Git

## Fluxo Básico de Trabalho (o mais usado no dia a dia)

Este é o ciclo que você vai repetir toda vez que fizer alterações no projeto:

```bash
git status                        # 1. Veja o que foi modificado
git add .                         # 2. Adicione TUDO ao stage
git commit -m "sua mensagem aqui" # 3. Registre as alterações com uma mensagem
git push origin main              # 4. Envie para o GitHub
```

> **Dica:** No passo 2, `git add .` adiciona todos os arquivos modificados de uma vez. Se quiser adicionar só um arquivo específico, use `git add nome-do-arquivo.html`.

---

## Visualizando o Histórico de Commits

### `git log` — Ver a lista completa de commits

```bash
git log
```
Exibe o histórico completo com hash, autor, data e mensagem de cada commit. Pressione **Q** para sair.

---

### `git log --oneline` — Ver o histórico de forma resumida ⭐ (mais usado)

```bash
git log --oneline
```
Exibe cada commit em uma linha, com o hash abreviado e a mensagem. Muito mais legível!

Exemplo de saída:
```
39dd858 (HEAD -> main) Mudando o titulo para portugues
237cada mudanças no titulo e gitignore
16018ad Create README.md
```

---

### `git log -p` — Ver o histórico com as alterações detalhadas

```bash
git log -p
```
Além das informações padrão, exibe o **diff** (o que foi adicionado e removido) em cada commit.
- Linhas com `-` = foram **removidas**
- Linhas com `+` = foram **adicionadas**

---

### `git log --graph` — Ver o histórico com ramificações visuais

```bash
git log --graph
```
Útil para visualizar branches (ramificações) graficamente no terminal.

---

### `git log --format="..."` — Personalizar o que aparece no log

```bash
git log --format="%H %an"
```
Exibe o hash completo (`%H`) e o nome do autor (`%an`) de cada commit. Use `git log --help` para ver todos os placeholders disponíveis.

---

## Inspecionando Commits Específicos

### `git show` — Ver os detalhes do último commit

```bash
git show
```
Sem argumentos, mostra os detalhes do **HEAD** (o commit mais recente).

---

### `git show <hash>` — Ver os detalhes de um commit específico

```bash
git show 2ad48c0
```
Substitua `2ad48c0` pelo hash do commit que deseja inspecionar (você pega esse hash com `git log --oneline`).

---

## Comparando Diferenças

### `git diff` — Ver o que foi alterado e ainda não foi adicionado

```bash
git diff
```
Compara o que você modificou nos arquivos com o **último commit**. Não mostra nada depois de `git add`, pois o arquivo já foi para o stage.

---

### `git diff <hash1>..<hash2>` — Comparar dois commits

```bash
git diff 5880fc1..5bc160e
```
Mostra todas as diferenças entre dois commits. Coloque o commit mais antigo primeiro e o mais novo depois.

---

### `git diff <hash>` — Comparar um commit com o estado atual

```bash
git diff 16018ad
```
Compara o commit informado com o HEAD (estado atual do projeto).

---

## Verificando o Status do Projeto

### `git status` — Ver o estado atual dos arquivos

```bash
git status
```
Mostra:
- Em qual branch você está
- Quais arquivos foram **modificados** (mas ainda não estão no stage)
- Quais arquivos estão no **stage** (prontos para o commit)
- Se não há nada para commitar

---

## Resumo Rápido — Tabela de Referência

| Comando | Para que serve |
|---|---|
| `git status` | Ver o que foi modificado no projeto |
| `git add .` | Adicionar todas as alterações ao stage |
| `git add arquivo.html` | Adicionar um arquivo específico ao stage |
| `git commit -m "mensagem"` | Registrar as alterações com uma mensagem |
| `git push origin main` | Enviar os commits para o GitHub |
| `git log` | Ver o histórico completo de commits |
| `git log --oneline` | Ver o histórico resumido (uma linha por commit) |
| `git log -p` | Ver o histórico com as alterações em cada commit |
| `git log --graph` | Ver o histórico com ramificações visuais |
| `git show` | Ver os detalhes do último commit |
| `git show <hash>` | Ver os detalhes de um commit específico |
| `git diff` | Ver o que foi alterado e ainda não foi para o stage |
| `git diff <hash1>..<hash2>` | Comparar dois commits entre si |
| `git diff <hash>` | Comparar um commit com o estado atual |

---

## Conceitos Importantes

**HEAD** — É um apelido para o commit mais recente da branch em que você está. Quando você vê `HEAD -> main` no log, significa que o commit atual é o topo da branch `main`.

**Stage (ou index)** — É uma área intermediária. Quando você faz `git add`, o arquivo vai para o stage. Ele fica "esperando" até você fazer o `git commit`.

**Hash** — É o identificador único de cada commit (aquele código como `237cada`). Você usa ele para se referir a um commit específico nos comandos `git show` e `git diff`.

**diff** — Formato que o Git usa para mostrar diferenças. Linhas com `-` foram removidas, linhas com `+` foram adicionadas.

---

## Próximos Tópicos do Curso

- Branches (ramificações) — criar, mesclar, navegar entre elas
- Git Merge e Git Rebase
- Guardando e desfazendo alterações
- Tags e releases no GitHub
- Comandos avançados: cherry-pick, blame
