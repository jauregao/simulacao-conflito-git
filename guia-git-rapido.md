# Guia rápido de Git e GitHub

Procure o que você quer fazer e siga os comandos na ordem.

Nos exemplos, a branch principal é `main` e a funcionalidade é `pagina-de-contato`.

## O que você quer fazer?

1. [Clonar um projeto](#1-clonar-um-projeto)
2. [Começar uma nova funcionalidade](#2-começar-uma-nova-funcionalidade)
3. [Criar um commit](#3-criar-um-commit)
4. [Enviar a branch ao GitHub](#4-enviar-a-branch-ao-github)
5. [Adicionar mais commits](#5-adicionar-mais-commits)
6. [Abrir um Pull Request](#6-abrir-um-pull-request)
7. [Corrigir um Pull Request](#7-corrigir-um-pull-request)
8. [Fazer um merge sem conflito](#8-fazer-um-merge-sem-conflito)
9. [Resolver um conflito](#9-resolver-um-conflito)
10. [Começar a próxima tarefa](#10-começar-a-próxima-tarefa)

---

## 1. Clonar um projeto

Use quando o projeto ainda não está no seu computador.

```bash
git clone https://github.com/usuario/nome-do-projeto.git
cd nome-do-projeto
```

- `git clone` baixa o projeto.
- `cd` entra na pasta do projeto.

Você só precisa clonar uma vez.

---

## 2. Começar uma nova funcionalidade

Entre na `main`, atualize e crie uma branch nova:

```bash
git checkout main
git pull origin main
git checkout -b pagina-de-contato
```

- `checkout main`: entra na branch principal.
- `pull`: traz as alterações mais recentes.
- `checkout -b`: cria a branch da funcionalidade e entra nela.

Use um nome curto que explique a tarefa, como `corrige-menu` ou `adiciona-formulario`.

---

## 3. Criar um commit

Depois de alterar e salvar os arquivos:

```bash
git status
git add .
git commit -m "Adiciona página de contato"
```

- `status`: mostra os arquivos alterados.
- `add .`: prepara as alterações.
- `commit`: registra as alterações no computador.

Escreva uma mensagem que diga o que foi feito.

---

## 4. Enviar a branch ao GitHub

Na primeira vez que enviar a branch:

```bash
git push -u origin pagina-de-contato
```

O `-u` conecta a branch do computador à branch do GitHub.

Nos próximos envios dessa branch, use apenas:

```bash
git push
```

---

## 5. Adicionar mais commits

Faça as novas alterações, salve e execute:

```bash
git status
git add .
git commit -m "Adiciona campos ao formulário"
git push
```

Se já existe um Pull Request dessa branch, ele será atualizado. Não abra outro.

---

## 6. Abrir um Pull Request

Depois de enviar a branch, abra o repositório no GitHub:

1. Clique em **Compare & pull request**.
2. Em **base**, escolha `main`.
3. Em **compare**, escolha `pagina-de-contato`.
4. Escreva um título que explique a mudança.
5. Descreva o que foi feito e como foi conferido.
6. Clique em **Create pull request**.

Exemplo de título:

```text
Adiciona página de contato
```

---

## 7. Corrigir um Pull Request

Entre na branch do Pull Request:

```bash
git checkout pagina-de-contato
```

Faça a correção, salve e envie outro commit:

```bash
git status
git add .
git commit -m "Corrige texto do formulário"
git push
```

O mesmo Pull Request será atualizado.

---

## 8. Fazer um merge sem conflito

No Pull Request do GitHub:

1. Confira se a branch pode ser mesclada.
2. Clique em **Merge pull request**.
3. Clique em **Confirm merge**.

Depois, atualize a `main` no computador:

```bash
git checkout main
git pull origin main
```

---

## 9. Resolver um conflito

Atualize a `main`:

```bash
git checkout main
git pull origin main
```

Volte para a branch da funcionalidade e traga a `main` para ela:

```bash
git checkout pagina-de-contato
git merge main
```

Veja os arquivos com conflito:

```bash
git status
```

Abra cada arquivo indicado. Você verá estas marcações:

- `<<<<<<< HEAD`: começa o conteúdo da sua branch;
- `=======`: separa as duas versões;
- `>>>>>>> main`: termina o conteúdo que veio da `main`.

Escolha o conteúdo correto e apague as três marcações.

Salve, confira o projeto e registre a resolução:

```bash
git add .
git commit -m "Resolve conflito com a main"
git push
```

Volte ao Pull Request. Quando o conflito desaparecer, faça o merge pelo GitHub.

---

## 10. Começar a próxima tarefa

Depois do merge, atualize a `main` e crie outra branch:

```bash
git checkout main
git pull origin main
git checkout -b nome-da-nova-tarefa
```

Use uma branch nova para cada tarefa.

---

## Ordem para lembrar

```text
clonar
→ atualizar a main
→ criar uma branch
→ alterar os arquivos
→ git add
→ git commit
→ git push
→ abrir o Pull Request
→ resolver conflitos, se existirem
→ fazer o merge
→ atualizar a main
```
