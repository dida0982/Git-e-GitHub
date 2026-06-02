# 🌿 Git: Branches, Checkout, Switch e Restore

> Resumo de estudo baseado no curso de Git & GitHub da Alura

---

## 🔍 Visualizando o Git graficamente

Antes de entrar nos comandos, vale a pena explorar o **[Visualizing Git](https://git-school.github.io/visualizing-git/)** — uma ferramenta interativa que simula operações do Git no navegador, sem precisar instalar nada.

**Por que usar?**
- Você digita comandos Git reais (`git commit`, `git branch`, `git merge`...)
- A ferramenta desenha o grafo de commits em tempo real
- Fica muito mais fácil entender o que acontece "por baixo dos panos"

**Exemplo prático:**
```
$ git commit -m "primeiro commit"
$ git branch feature
$ git checkout feature
$ git commit -m "novo recurso"
```
Ao digitar isso no Visualizing Git, você vê visualmente as duas branches se separando. 📊

---

## 🌳 O que são Branches?

Pense nas branches como **linhas do tempo paralelas** do seu projeto.

```
main:    A --- B --- C
                      \
feature:               D --- E
```

- `main` é a linha principal (produção)
- `feature` é uma ramificação onde você desenvolve algo novo sem afetar o `main`
- Quando terminar, você une as duas com `git merge`

**Comandos básicos de branch:**
```bash
git branch                   # lista todas as branches
git branch nome-da-branch    # cria uma nova branch
git branch -d nome-da-branch # deleta uma branch (após merge)
```

---

## 🔄 `git checkout` — O comando "canivete suíço" (e por que ele foi dividido)

O `git checkout` era usado para **várias coisas ao mesmo tempo**, o que o tornava confuso:

| Uso | Comando |
|-----|---------|
| Trocar de branch | `git checkout nome-da-branch` |
| Criar e já entrar em uma branch | `git checkout -b nova-branch` |
| Restaurar arquivo para versão anterior | `git checkout -- arquivo.txt` |
| Ir para um commit específico | `git checkout abc1234` |

Essa mistura de responsabilidades gerava confusão. Por isso, a partir do **Git 2.23**, o comando foi dividido em dois mais simples e intuitivos.

> ⚠️ O `git checkout` **continua funcionando normalmente** e não há planos de removê-lo. A divisão foi uma melhoria, não uma substituição obrigatória.

---

## 🔀 `git switch` — Trocar de branch com clareza

O `git switch` foi criado especificamente para **navegar entre branches**.

```bash
git switch nome-da-branch       # vai para uma branch existente
git switch -c nova-branch       # cria e já entra na branch (-c = create)
git switch -                    # volta para a branch anterior (atalho útil!)
```

**Comparação direta:**
```bash
# Forma antiga
git checkout feature

# Forma nova (mais clara)
git switch feature
```

---

## ♻️ `git restore` — Restaurar arquivos com clareza

O `git restore` foi criado para **descartar mudanças em arquivos** (a outra responsabilidade do `checkout`).

```bash
git restore arquivo.txt              # descarta mudanças no working directory
git restore --staged arquivo.txt     # remove arquivo da staging area (desfaz git add)
git restore --source=HEAD~1 arquivo.txt  # restaura versão de um commit específico
```

**Comparação direta:**
```bash
# Forma antiga
git checkout -- arquivo.txt

# Forma nova (mais clara)
git restore arquivo.txt
```

---

## 📊 Resumo visual: qual comando usar?

```
Quero...
│
├── Trocar de branch?
│   └── git switch nome-da-branch
│
├── Criar e entrar em nova branch?
│   └── git switch -c nova-branch
│
└── Desfazer mudanças em arquivo?
    ├── Ainda não fiz git add → git restore arquivo.txt
    └── Já fiz git add → git restore --staged arquivo.txt
```

---

## 🧩 Fluxo completo: do início ao merge

```bash
# 1. Criar e entrar na branch de feature
git switch -c feature/login

# 2. Fazer alterações e commits
git add .
git commit -m "Adiciona tela de login"

# 3. Voltar para a main
git switch main

# 4. Unir as mudanças
git merge feature/login

# 5. Deletar a branch (opcional, já foi mergeada)
git branch -d feature/login
```

---

## 📚 Recursos para aprofundar

- 🎮 [Visualizing Git](https://git-school.github.io/visualizing-git/) — playground visual de Git
- 📖 [Documentação oficial: git switch](https://git-scm.com/docs/git-switch)
- 📖 [Documentação oficial: git restore](https://git-scm.com/docs/git-restore)
- 🎓 [Alura+: Entenda os comandos git restore e switch](https://cursos.alura.com.br/extra/alura-mais/entenda-os-comandos-git-restore-e-switch-c99)

---

*Notas de estudo — Curso Git & GitHub: Dominando Controle de Versão de Código (Alura)*
