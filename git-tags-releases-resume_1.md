# 🏷️ Git Tags e GitHub Releases — Versionando seu Projeto

> Resumo de estudo baseado no curso de Git & GitHub da Alura

---

## 🎮 A analogia do Save Point

Pense nos commits do Git como um jogo com checkpoints. As **tags** são os *save points* nomeados — pontos específicos do histórico que você marca e diz: *"aqui estava a versão 1.0!"*

```
commits:   A --- B --- C --- D --- E
                 ↑               ↑
              tag: v0.1.0     tag: v0.1.1
              (save point!)   (save point!)
```

Diferente de uma branch, **a tag nunca se move**. Ela sempre aponta para o mesmo commit, para sempre.

---

## 🔖 Tags simples (Lightweight Tags)

Uma tag simples é apenas um **apelido** para um commit — nada mais.

```bash
git tag v0.1.0                    # cria tag na HEAD (commit atual)
git tag v0.1.1 502afb6            # cria tag em um commit específico (pelo hash)
git tag                           # lista todas as tags
git log --oneline                 # mostra tags no histórico
```

Exemplo de saída do `git log --oneline`:
```
502afbc (HEAD -> main, tag: v0.1.1) Removendo quebra de linha
c53eb16 (tag: v0.1.0) Quebrando linha do script
bc493a6 Corrigindo indentação
```

---

## 📝 Annotated Tags — Tags com informações extras

Uma **annotated tag** vai além do apelido: ela armazena mensagem, autor e data de criação próprios, independente do commit que ela aponta.

| | Tag simples | Annotated Tag |
|--|:-----------:|:-------------:|
| Aponta para um commit | ✅ | ✅ |
| Tem mensagem própria | ❌ | ✅ |
| Guarda autor e data | ❌ | ✅ |
| Pode ser verificada com `-v` | ❌ | ✅ |

### Criando uma annotated tag

```bash
git tag -a v0.1.1 -m "Lançamento da versão 0.1.1"
#        ↑              ↑
#    annotated       mensagem
```

> 💡 O `-a` é opcional! Se você usar `-m` (mensagem), o Git já entende que é annotated:
> ```bash
> git tag v0.1.1 -m "Lançamento da versão 0.1.1"   # funciona igual
> ```

### Inspecionando uma annotated tag

```bash
git tag -v v0.1.1
```

Saída mostra: o commit que ela aponta, o autor, a data e a mensagem da tag.

---

## 🗑️ Apagando tags

```bash
# Localmente
git tag -d v0.1.1

# No repositório remoto (GitHub)
# Pode ser feito pela interface do GitHub (⋯ > Delete tag)
# Ou via terminal:
git push origin --delete v0.1.1
```

---

## 📤 Enviando tags para o GitHub

Por padrão, `git push` **não envia tags**. Você precisa fazer isso explicitamente:

```bash
git push origin v0.1.1        # envia uma tag específica
git push origin --tags        # envia TODAS as tags de uma vez
```

---

## 🚀 Releases no GitHub

Uma **release** é uma publicação de versão no GitHub, construída a partir de uma tag. É onde você anuncia oficialmente uma nova versão do projeto.

### O que uma release oferece:

```
📦 Release v0.1.1 — "Lançamento da versão 0.1.1"
│
├── 📋 Release notes (changelog automático ou manual)
│     └── Link mostrando o diff entre v0.1.0 e v0.1.1
│
└── 📎 Assets (arquivos para download)
      ├── projeto.zip      ← código-fonte compactado (automático)
      ├── projeto.tar.gz   ← código-fonte compactado (automático)
      └── app.exe          ← binário compilado (você adiciona, se houver)
```

> Os arquivos `.zip` e `.tar.gz` são gerados **automaticamente** pelo GitHub com o código-fonte daquela versão — úteis para quem não usa Git.

### Como criar uma release manualmente

1. No GitHub, acesse a aba **Releases** → **"Create a new release"**
2. Escolha uma **tag existente** (ou crie uma nova)
3. Defina um **título** para a release
4. Escreva as **release notes** (ou clique em "Generate release notes" para gerar automaticamente)
5. Anexe **arquivos binários** se necessário (`.exe`, `.jar`, etc.)
6. Clique em **"Publish release"**

---

## 🔄 Fluxo completo: do commit à release

```bash
# 1. Seu projeto está em um estado estável
git log --oneline
# abc1234 (HEAD -> main) Correção de bug crítico
# def5678 Adiciona autenticação

# 2. Cria a tag no commit atual
git tag v1.0.0 -m "Primeira versão estável"

# 3. Envia a tag para o GitHub
git push origin v1.0.0

# 4. No GitHub: cria a release a partir da tag v1.0.0
# (adiciona changelog, binários, etc.)
```

---

## 📊 Resumo dos comandos

| Comando | O que faz |
|---------|-----------|
| `git tag v1.0.0` | Cria tag simples na HEAD |
| `git tag v1.0.0 abc1234` | Cria tag simples em commit específico |
| `git tag v1.0.0 -m "msg"` | Cria annotated tag com mensagem |
| `git tag -a v1.0.0 -m "msg"` | Idem (com `-a` explícito) |
| `git tag` | Lista todas as tags |
| `git tag -v v1.0.0` | Inspeciona uma annotated tag |
| `git tag -d v1.0.0` | Apaga tag localmente |
| `git push origin v1.0.0` | Envia tag específica ao GitHub |
| `git push origin --tags` | Envia todas as tags ao GitHub |

---

## 📚 Recursos para aprofundar

- 📖 [Documentação oficial: git tag](https://git-scm.com/docs/git-tag)
- 📖 [GitHub Docs: Managing releases](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)

---

*Notas de estudo — Curso Git & GitHub: Dominando Controle de Versão de Código (Alura)*
