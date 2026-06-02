# ⏪ Git: Desfazendo Alterações — `restore` e `stash`

> Resumo de estudo baseado no curso de Git & GitHub da Alura

---

## 🗺️ O mapa do território: Working Tree vs Staging Area

Antes de entender os comandos, é essencial saber **onde** suas alterações estão:

```
┌─────────────────────────────────────────────────────────┐
│                     SEU PROJETO                         │
│                                                         │
│  📁 Working Tree          📦 Staging Area    💾 Commit  │
│  (arquivos editados)  ──► (após git add)  ──► (salvo)   │
│                                                         │
│  git status: vermelho      git status: verde            │
└─────────────────────────────────────────────────────────┘
```

| Área | O que é | Como chegar lá |
|------|---------|----------------|
| **Working Tree** | Seus arquivos com modificações ainda não adicionadas | Só editar o arquivo |
| **Staging Area** | O que está pronto para o próximo commit | `git add arquivo.txt` |
| **Commit** | Snapshot salvo permanentemente no histórico | `git commit -m "..."` |

---

## ♻️ `git restore` — Desfazendo alterações

O `git restore` é o comando para **voltar arquivos a um estado anterior**. Ele atua em dois cenários diferentes dependendo dos parâmetros usados.

### Cenário 1: Desfazer alterações na Working Tree

Você editou um arquivo mas **ainda não fez `git add`** e quer descartar a mudança:

```bash
git restore arquivo.txt       # desfaz alterações em um arquivo específico
git restore .                 # desfaz alterações em TODO o projeto (ponto = diretório atual)
```

> 💡 Equivalente ao velho `git checkout -- arquivo.txt`

**Analogia:** É como apertar `Ctrl+Z` no projeto inteiro. Útil quando você percebe que uma implementação estava errada e quer começar do zero.

---

### Cenário 2: Remover arquivo da Staging Area

Você já fez `git add` mas **mudou de ideia** e não quer incluir esse arquivo no próximo commit:

```bash
git restore --staged arquivo.txt    # tira o arquivo do "palco", mas mantém as mudanças
```

> ⚠️ Isso **NÃO desfaz** as alterações no código — apenas move o arquivo de volta para a Working Tree. As mudanças continuam lá, só saem do palco.

```
ANTES:  [Staging Area: app.js ✅]  →  git restore --staged app.js
DEPOIS: [Working Tree: app.js 📝]  →  alterações ainda existem, mas fora do stage
```

---

### Cenário 3: "Viajar no tempo" para um commit específico

Quer ver (ou restaurar) como um arquivo estava em um commit antigo?

```bash
# Copie o hash do commit com git log, então:
git restore --source=5081a55bc92af2917c8519f16a7412b86ba3b1c2 index.html
```

Depois de explorar, para voltar ao estado atual:
```bash
git restore index.html    # equivalente a --source=HEAD (último commit)
```

---

### Resumo visual do `git restore`

```
                    ┌──────────────────────────────────────┐
                    │           git restore                │
                    └──────────────────────────────────────┘
                                     │
           ┌─────────────────────────┼─────────────────────────┐
           │                         │                         │
    sem parâmetro             --staged                  --source=HASH
           │                         │                         │
   Desfaz mudanças na        Tira do stage,           Restaura arquivo
    Working Tree              mantém mudanças          para commit X
  (apaga o que você fez)    (volta ao vermelho)       (viagem no tempo)
```

---

## 🗄️ `git stash` — A gaveta de trabalhos em progresso

### O problema que o stash resolve

Imagine: você está **no meio de uma funcionalidade**, o código está incompleto (não compila, não está funcional). De repente, surge um **bug urgente** que precisa ser resolvido agora.

Você não pode:
- Fazer commit (código incompleto ≠ bom commit)
- Trocar de branch com arquivos modificados (o Git vai reclamar)

**Solução:** guardar o trabalho na "gaveta" com `git stash` e retomá-lo depois.

---

### Comandos do `git stash`

#### Guardando alterações

```bash
git stash                          # guarda tudo com nome automático (WIP...)
git stash push -m "descrição"      # guarda com nome descritivo (recomendado!)
```

#### Consultando o que está guardado

```bash
git stash list                     # lista tudo na gaveta
```

Exemplo de saída:
```
stash@{0}: On main: Removendo quebras de linha
stash@{1}: On movendo-detalhes: Movendo chamada de função
```

> O índice `{0}` é sempre o item mais recente (conceito de **pilha**).

#### Recuperando alterações

| Comando | O que faz | Remove da stash? |
|---------|-----------|:----------------:|
| `git stash pop` | Aplica o item mais recente (índice 0) | ✅ Sim |
| `git stash pop 1` | Aplica o item de índice 1 | ✅ Sim |
| `git stash apply 1` | Aplica o item de índice 1 | ❌ Não |
| `git stash drop` | Remove o item mais recente SEM aplicar | ✅ Sim |
| `git stash drop 1` | Remove o item de índice 1 SEM aplicar | ✅ Sim |
| `git stash clear` | Apaga TUDO da stash | ✅ Sim (tudo) |

---

### O conceito de pilha 🥞

A stash funciona como uma **pilha de pratos**:

```
git stash       →  coloca um prato em cima
git stash       →  coloca mais um prato em cima
git stash pop   →  pega o prato do TOPO (o último adicionado)
```

```
Stash (pilha):
┌─────────────────────────────────┐
│ [0] Removendo quebras de linha  │  ← pop/drop age aqui primeiro
│ [1] Movendo chamada de função   │
└─────────────────────────────────┘
```

Para pegar um item específico que não seja o do topo, use o índice:
```bash
git stash apply 1    # aplica item de índice 1, mantém na stash
git stash pop 1      # aplica item de índice 1, remove da stash
```

---

### Fluxo completo: usando stash no dia a dia

```bash
# 1. Você está trabalhando em uma feature
git switch -c feature/novo-recurso
# ... edita arquivos ...

# 2. Bug urgente surge! Guarda o trabalho
git stash push -m "WIP: movendo chamada de função"

# 3. Vai para a main e corrige o bug
git switch main
# ... corrige o bug, faz commit ...

# 4. Volta para a feature e recupera o trabalho
git switch feature/novo-recurso
git stash pop

# 5. Continua de onde parou!
```

---

## 🔄 `git restore` vs `git stash` — Quando usar cada um?

| Situação | Comando |
|----------|---------|
| Quero **apagar** minhas mudanças (não precisarei delas) | `git restore .` |
| Quero **pausar** o trabalho e retomar depois | `git stash` |
| Fiz `git add` mas mudei de ideia | `git restore --staged arquivo` |
| Quero ver como um arquivo era em commit antigo | `git restore --source=HASH arquivo` |
| Quero descartar um item guardado na stash | `git stash drop` |
| Quero limpar toda a stash | `git stash clear` |

---

## 📚 Recursos para aprofundar

- 📖 [Documentação oficial: git restore](https://git-scm.com/docs/git-restore)
- 📖 [Documentação oficial: git stash](https://git-scm.com/docs/git-stash)
- 🎓 [Alura+: Entenda os comandos git restore e switch](https://cursos.alura.com.br/extra/alura-mais/entenda-os-comandos-git-restore-e-switch-c99)

---

*Notas de estudo — Curso Git & GitHub: Dominando Controle de Versão de Código (Alura)*
