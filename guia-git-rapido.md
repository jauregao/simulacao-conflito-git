# Git em equipe — guia rápido com passo a passo

**Tarefa do exemplo:** adicionar uma seção de contato ao site, trabalhar na branch `contato` e propor a entrada dessa mudança na `main`.

Para entender os conceitos com calma, leia o [guia aprofundado](guia-git-aprofundado.md).

## Antes de começar

- O projeto já deve estar no computador, com Git configurado e acesso de envio ao repositório da turma no GitHub.
- Abra o terminal na raiz do projeto: a pasta principal que contém os arquivos do site.
- Neste exemplo, a branch principal se chama `main` e o remoto se chama `origin`. Use os nomes combinados para o projeto se forem diferentes.
- Execute **uma etapa de cada vez**. Se um comando falhar, leia a mensagem com a pessoa instrutora antes de seguir.

## 1. Confira se pode começar uma tarefa nova

```bash
git status
```

**O que faz:** mostra a branch atual e se existem mudanças pendentes. Não modifica arquivos.

**Confira:** comece sem alterações pendentes (`nothing to commit, working tree clean`). Se aparecer trabalho anterior, conclua esse trabalho na branch correta com orientação antes de trocar de branch.

## 2. Entre na principal e atualize

```bash
git checkout main
git pull origin main
```

- `git checkout main`: muda para a branch principal no computador.
- `git pull origin main`: busca a `main` do GitHub e integra suas mudanças à branch atual. `origin` é o apelido do repositório remoto.

**Por quê:** a tarefa nova deve começar com o trabalho que a equipe já incorporou. Neste roteiro, não fazemos commits diretamente na `main`.

## 3. Crie a branch da tarefa

```bash
git checkout -b contato
```

**O que faz:** `-b` cria a branch `contato` a partir do ponto atual e já entra nela. Seus novos commits serão feitos nessa branch.

**Confira com `git status`:** deve aparecer `On branch contato`.

Se você está retomando essa tarefa e a branch já existe, use `git checkout contato`: ele apenas entra na branch existente, sem criar outra.

## 4. Faça a alteração e confira o site

No editor, adicione a seção de contato no local adequado da página. Salve o arquivo e abra a página no navegador para conferir o resultado.

```bash
git status
```

**O que faz:** permite conferir quais arquivos foram alterados antes de preparar o commit. Verifique se pertencem à tarefa.

## 5. Prepare e registre a mudança

```bash
git add .
git commit -m "Adiciona seção de contato"
```

- `git add .`: prepara as mudanças da pasta atual e de suas subpastas para o commit, incluindo exclusões. Por isso, confira os arquivos antes de usar o ponto.
- `git commit`: registra as mudanças preparadas no histórico local.
- `-m`: permite informar a mensagem entre aspas. Escreva o que foi feito.

**Lembrete:** se editar novamente depois do `add`, salve e repita o `add` antes do commit para incluir a nova edição. Salvar, preparar e registrar são etapas diferentes.

## 6. Envie a branch para o GitHub

```bash
git push -u origin contato
```

**O que faz:** envia os commits da `contato` para o remoto `origin`. O `-u` associa essa branch local à remota, permitindo usar apenas `git push` nos próximos envios dela.

**Confira:** o envio deve terminar com sucesso. O trabalho está na branch `contato` do GitHub; a integração na `main` vem depois da revisão.

## 7. Abra o Pull Request no GitHub

1. Abra o repositório da turma e inicie a criação de um Pull Request (PR).
2. Escolha **destino/base: `main`** e **origem/compare: `contato`**.
3. Confira se a comparação mostra somente as mudanças esperadas para a tarefa.
4. Escreva o título “Adiciona seção de contato”. Na descrição, diga o que mudou e o que você conferiu no navegador.
5. Crie o PR e combine a revisão com a dupla ou com a pessoa instrutora.

**O que faz:** propõe incorporar a tarefa na `main` e permite que outra pessoa revise. Abrir o PR ainda não realiza essa integração.

## 8. Se pedirem ajustes

Continue na `contato`. Corrija o que foi combinado, salve e confira a página. Depois:

```bash
git status
git add .
git commit -m "Corrige e-mail de contato"
git push
```

**O que cada comando faz:** `status` confere a situação; `add` prepara a correção; `commit` a registra; `push` a envia. Adapte a mensagem à correção realizada.

**Confira:** os novos commits aparecem no mesmo PR aberto. Não é necessário criar outro.

## 9. Depois da revisão e do merge

A pessoa responsável conclui o **merge** do PR no GitHub: incorpora as mudanças na `main`. Se houver conflito, use a seção abaixo antes de concluir o PR.

Depois que o PR estiver integrado, sem alterações locais pendentes, execute:

```bash
git checkout main
git pull origin main
```

**O que fazem:** o `checkout` entra na principal local e o `pull` traz a versão do GitHub, agora com a tarefa integrada. Confira a seção de contato na página. Comece a próxima tarefa criando outra branch a partir dessa `main` atualizada.

## Se aparecer um conflito no PR

Use este trecho com a pessoa instrutora. **Antes, registre e envie suas alterações da `contato`; o `git status` deve indicar que não há mudanças pendentes.**

### A. Traga a principal para a tarefa

```bash
git checkout main
git pull origin main
git checkout contato
git merge main
```

1. `checkout main` entra na principal local.
2. `pull origin main` atualiza essa principal com o GitHub.
3. `checkout contato` volta à tarefa.
4. `merge main` incorpora a principal local à branch atual, `contato`.

### B. Resolva os arquivos indicados

Execute `git status` para consultar os arquivos em conflito. Abra-os no editor. Um trecho pode aparecer assim:

```text
<<<<<<< HEAD
<h2>Fale com a equipe</h2>
=======
<h2>Entre em contato</h2>
>>>>>>> main
```

A parte de cima é a da `contato`; a de baixo veio da `main`. Converse com a dupla sobre o resultado correto. Edite para deixar apenas o conteúdo final, sem as três linhas de marcação. Resolva todos os trechos, salve e confira a página no navegador.

### C. Registre e envie a resolução

```bash
git add .
git commit -m "Resolve conflito no título de contato"
git push
```

**O que fazem:** `add` prepara os arquivos resolvidos, `commit` conclui o merge pendente e `push` envia o resultado ao mesmo PR. Volte à revisão no GitHub.

Se `git merge main` concluir sem conflito, pule a edição de marcações e o commit de resolução. Se abrir um editor para a mensagem do merge, conclua-o com a pessoa instrutora. Confira a página e faça `git push` para enviar eventuais commits novos.

## Para lembrar durante a prática

**Salvar no editor → `add` prepara → `commit` registra no computador → `push` envia → PR pede revisão → merge incorpora na principal → `pull` atualiza a principal local.**
