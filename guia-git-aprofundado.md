# Git em equipe — guia aprofundado para leitura em aula

Este material explica o que acontece em cada etapa do trabalho com Git. Vamos acompanhar uma única situação: **Ana e Bruno estão trabalhando no mesmo site, e Ana precisa adicionar uma seção de contato.**

Depois da leitura, use o [guia rápido com o passo a passo](guia-git-rapido.md) para praticar.

## 1. O site funciona. Como continuar trabalhando nele em equipe?

Imagine que Ana vai criar a seção de contato enquanto Bruno ajusta o menu. O site já tem uma versão que funciona, mas as duas tarefas ainda estão em andamento.

Se cada pessoa mandar uma pasta chamada `site-final`, como saber qual contém as mudanças mais recentes? E se Ana substituir um arquivo que Bruno acabou de alterar?

O Git ajuda a registrar as mudanças no projeto. Com esses registros, a equipe consegue acompanhar o trabalho e combinar alterações. Para entender esse processo, vamos começar pelos comandos que vocês já usam.

## 2. O que existe no computador e o que existe no GitHub?

A pasta do projeto no computador contém os arquivos que você abre e edita. Quando essa pasta é acompanhada pelo Git, ela faz parte de um **repositório**: o projeto com seu histórico de alterações registradas.

Neste exemplo, a equipe também tem um repositório no GitHub. Ele é o lugar compartilhado para enviar o trabalho e receber as mudanças das outras pessoas.

- **Local:** o repositório no seu computador.
- **Remoto:** o repositório compartilhado, neste caso hospedado no GitHub.

Git e GitHub têm funções diferentes: **Git é a ferramenta que registra e organiza as mudanças; GitHub é a plataforma onde a equipe compartilha o repositório e revisa contribuições.** Você pode fazer um commit no computador sem estar conectado à internet. Para enviar esse commit ao GitHub, precisa de conexão.

Nos comandos desta aula, `origin` é o apelido que o Git usa para o endereço do repositório remoto. Não é o nome de uma pasta nem de uma pessoa.

## 3. Salvar, adicionar, fazer commit e enviar: o que muda?

Ana escreveu uma seção de contato no arquivo `index.html`. Ela salvou o arquivo no editor. O que aconteceu?

O arquivo no computador foi atualizado. **Salvar no editor não cria um commit e não envia a mudança ao GitHub.** Ainda há outras etapas.

### Primeiro: conferir a situação com `git status`

```bash
git status
```

O comando mostra a branch atual e a situação das mudanças: quais arquivos foram alterados, quais já estão preparados para um commit e quais ainda não são acompanhados pelo Git. Ele apenas consulta; não altera os arquivos.

Algumas mensagens que podem aparecer:

| Mensagem | Como entender |
| --- | --- |
| `On branch contato` | Você está trabalhando na branch chamada `contato`. Vamos entender branches na próxima seção. |
| `Changes not staged for commit` | Há mudanças que ainda não foram selecionadas para o próximo commit. |
| `Changes to be committed` | Há mudanças selecionadas para o próximo commit. |
| `Untracked files` | Há arquivos novos que o Git ainda não acompanha. |
| `nothing to commit, working tree clean` | Não há mudanças locais pendentes para registrar. Isso, sozinho, não confirma que tudo foi enviado ao GitHub. |

### Depois: selecionar as mudanças com `git add`

```bash
git add .
```

O `add` prepara mudanças para o próximo commit. O ponto significa “a partir desta pasta e das pastas dentro dela”. Executado na raiz do projeto, seleciona as mudanças de todo o projeto que o Git pode adicionar, incluindo arquivos novos, modificações e exclusões. Arquivos configurados para serem ignorados normalmente ficam de fora.

Essa seleção é chamada de **área de preparação**. Pense nela como a lista do que vai entrar no próximo registro.

Por isso, olhamos o `status` antes: se Ana alterou sem querer outro arquivo, o ponto também pode selecioná-lo. Neste exercício, só devemos ter mudanças da tarefa de contato.

**Atenção à ordem:** o `add` seleciona o conteúdo naquele momento. Se Ana editar o arquivo novamente depois, precisa salvar e executar o `add` outra vez para incluir a nova edição no próximo commit.

### Em seguida: registrar com `git commit`

```bash
git commit -m "Adiciona seção de contato"
```

Um **commit** é um registro no histórico do projeto. Esse comando registra as mudanças que foram preparadas com `add`.

- `git commit` cria o registro no repositório local.
- `-m` permite escrever a mensagem do commit no próprio comando.
- O texto entre aspas explica o que foi feito.

Uma mensagem como “Adiciona seção de contato” ajuda a equipe a entender a mudança. “Coisas” ou “Alterações” não explica o trabalho realizado.

Fazer commit não envia o trabalho ao GitHub. Ele fica registrado no computador até ser enviado.

### Por último: enviar com `git push`

```bash
git push -u origin contato
```

Esse comando envia os commits da branch `contato` ao repositório remoto chamado `origin`.

- `push` envia os commits.
- `origin` indica para qual repositório remoto enviar.
- `contato` indica a branch que será enviada.
- `-u` associa a branch local à branch remota correspondente. Depois dessa primeira configuração, estando na branch `contato`, podemos usar apenas `git push` nos próximos envios.

O `push` envia commits. Ele não inclui uma edição que ficou apenas salva no editor, sem commit.

### Acompanhe a mesma mudança

| Ana acabou de… | Onde está a mudança? | Já chegou ao GitHub? |
| --- | --- | --- |
| Salvar no editor | No arquivo do computador | Não |
| Executar `git add .` | No arquivo e na seleção para o próximo commit | Não |
| Fazer commit | Registrada no histórico local | Não |
| Fazer push com sucesso | Também no histórico da branch remota | Sim |

**Para conversar:** Ana fez um commit e desligou o computador sem fazer push. Bruno consegue receber esse commit do GitHub? Por quê?

## 4. O que é uma branch e por que vamos usá-la?

Ana precisa experimentar a seção de contato sem colocar uma tarefa incompleta na versão compartilhada que a equipe usa como referência.

Para isso, ela cria uma **branch**, uma linha de trabalho dentro do repositório. A branch permite registrar os commits da tarefa separadamente da linha principal.

Neste projeto, a branch principal se chama `main`. A equipe combina que ela receberá as tarefas depois da revisão. O nome `main` não garante que o código funciona: manter essa versão revisada é uma responsabilidade da equipe.

Ana cria a branch `contato` a partir da `main`. Nesse momento, as duas partem do mesmo histórico. Depois, os novos commits que Ana fizer na `contato` pertencem a essa linha de trabalho e ainda não entram na `main`.

```text
main:     versão inicial ─────────────────── versão compartilhada
                        \
contato:                 adiciona contato ── ajusta texto
```

Não é necessário criar outra pasta do site. Ao trocar de branch, o Git atualiza os arquivos da pasta para refletir a linha de trabalho escolhida. Por isso, uma seção que já foi registrada na `contato` pode deixar de aparecer ao voltar para a `main`: ela ainda não foi incorporada ali.

### Trocar para uma branch que já existe

```bash
git checkout main
```

O comando muda a branch atual para `main`. Ele não baixa as novidades do GitHub; apenas troca a linha de trabalho no computador.

### Criar uma branch e começar a trabalhar nela

```bash
git checkout -b contato
```

O `-b` pede para criar uma branch nova. O comando cria `contato` a partir do ponto atual e já muda para ela. Por isso, vamos executá-lo depois de entrar na `main` e atualizá-la.

Se a branch `contato` já existir, para voltar a ela usamos:

```bash
git checkout contato
```

**Antes de trocar de branch, confira o `git status`.** Neste roteiro, vamos trocar somente sem mudanças pendentes. Alterações sem commit podem acompanhar a troca ou impedir o comando; criar uma branch, sozinho, não registra nem guarda essas alterações.

**Para conversar:** Ana fez commit e push na `contato`. A seção já entrou na `main`? Qual é a diferença entre compartilhar uma tarefa e incorporá-la à versão principal?

## 5. Por que usar `pull` antes de começar?

Bruno terminou o menu, e a mudança dele já entrou na `main` do GitHub. A `main` do computador de Ana ainda pode estar antiga.

Para começar a tarefa com as mudanças compartilhadas mais recentes, Ana executa:

```bash
git checkout main
git pull origin main
```

O primeiro comando entra na `main` local. O segundo busca as novidades da `main` do remoto `origin` e as integra à branch em que Ana está.

**O `pull` atua sobre a branch atual.** Escrever `main` no final não faz o Git trocar para ela. É por isso que a troca vem antes.

Neste roteiro, ninguém faz commits diretamente na `main` local. As tarefas são feitas em branches próprias, e a `main` é atualizada a partir do GitHub. Se o `pull` apresentar um erro ou pedir uma decisão inesperada, pare e leia a mensagem com a pessoa instrutora antes de continuar.

Uma forma de lembrar:

- `push`: envia commits do computador para o remoto.
- `pull`: busca mudanças do remoto e as integra no computador.

## 6. O que é um Pull Request?

Ana terminou a seção, conferiu o resultado no navegador e enviou a branch `contato` ao GitHub. Agora Bruno precisa revisar antes de a tarefa entrar na `main`.

Ana abre um **Pull Request**, também chamado de **PR**. É uma proposta para incorporar as mudanças de uma branch em outra, com espaço para a equipe ler o código, comentar e pedir ajustes.

Neste caso, a proposta é:

```text
contato → main
de onde vêm as mudanças → para onde elas devem ir
```

Na criação do PR, a branch de destino, ou **base**, deve ser `main`. A branch com as mudanças, ou **compare**, deve ser `contato`.

Um título e uma descrição possíveis:

> **Título:** Adiciona seção de contato  
> **Descrição:** Inclui título e e-mail de contato no final da página. Conferi no navegador se a seção aparece e se o menu continua funcionando.

Abrir o PR não incorpora automaticamente a tarefa na `main`. Ele fica disponível para revisão.

**Pull e Pull Request são coisas diferentes.** `git pull` é um comando para buscar e integrar mudanças no repositório local. O Pull Request é uma proposta de integração e revisão feita na plataforma, neste caso o GitHub.

### E se Bruno pedir uma correção?

Ana continua na branch `contato`, faz a correção, salva e registra outro commit:

```bash
git add .
git commit -m "Corrige e-mail de contato"
git push
```

Aqui, `add` prepara a correção, `commit` a registra e `push` envia o novo registro. O envio curto funciona porque Ana já usou `-u` no primeiro push dessa branch.

**O mesmo PR aberto recebe os novos commits enviados à mesma branch.** Não é preciso abrir outro PR para atender a essa revisão.

## 7. O que é merge?

Depois da revisão e dos ajustes, a pessoa responsável pode concluir a integração da tarefa pelo GitHub. Essa integração é chamada de **merge**: combinar as mudanças de uma linha de trabalho com outra.

No nosso caso, o resultado da seção de contato passa a fazer parte da `main` no GitHub.

Observe as três etapas:

| Etapa | O que acontece? |
| --- | --- |
| Push da `contato` | A tarefa é compartilhada na branch remota `contato`. |
| Abertura do PR | A equipe recebe a proposta de incorporar a tarefa na `main`. |
| Merge do PR | As mudanças são incorporadas à `main` remota. |

A `main` no computador ainda precisa ser atualizada. Sem alterações pendentes, Ana executa:

```bash
git checkout main
git pull origin main
```

O `checkout` entra na `main` local. O `pull` traz e integra a versão remota que agora inclui a seção de contato. Para outra tarefa, Ana criará outra branch a partir dessa `main` atualizada.

## 8. O que é um conflito?

Enquanto Ana trabalhava, Bruno também alterou o título da seção no mesmo arquivo. As duas mudanças partiram de um título antigo:

```html
<h2>Contato</h2>
```

Na branch de Ana, ficou:

```html
<h2>Fale com a equipe</h2>
```

Na `main`, depois de uma contribuição de Bruno, ficou:

```html
<h2>Entre em contato</h2>
```

Ao combinar essas alterações, o Git pode não conseguir decidir qual texto deve permanecer. Isso é um **conflito**: uma situação que precisa de uma decisão humana para concluir a integração.

Não basta duas pessoas editarem o mesmo arquivo para haver conflito. Muitas alterações em trechos diferentes podem ser combinadas automaticamente. O exemplo acima mexe na mesma linha de duas maneiras diferentes.

### Trazer a `main` para a tarefa

Antes deste procedimento, Ana deve ter registrado e enviado suas mudanças da `contato`, sem alterações pendentes. Ela executa um comando de cada vez:

```bash
git checkout main
git pull origin main
git checkout contato
git merge main
```

| Comando | O que faz e por que vem aqui? |
| --- | --- |
| `git checkout main` | Entra na principal local para atualizá-la. |
| `git pull origin main` | Busca e integra a principal do GitHub. |
| `git checkout contato` | Volta à tarefa que precisa receber essas novidades. |
| `git merge main` | Incorpora as mudanças da `main` local à branch atual, que é `contato`. |

**A direção importa:** estando na `contato`, `git merge main` traz a `main` para `contato`. Esse comando não coloca a tarefa na `main`; isso continuará sendo feito pelo PR.

### Ler e resolver as marcações

Se houver conflito, o Git interrompe a conclusão do merge e indica os arquivos envolvidos. O `git status` ajuda a localizá-los. Dentro do arquivo, o trecho pode aparecer assim:

```text
<<<<<<< HEAD
<h2>Fale com a equipe</h2>
=======
<h2>Entre em contato</h2>
>>>>>>> main
```

- Entre `<<<<<<< HEAD` e `=======` está a versão da branch atual, neste caso `contato`.
- Entre `=======` e `>>>>>>> main` está a versão trazida da `main`.
- As três linhas de marcação delimitam o conflito. Elas não devem permanecer no arquivo final.

Ana e Bruno combinam que o título será “Fale com a equipe”. Ana edita o trecho até restar somente:

```html
<h2>Fale com a equipe</h2>
```

Resolver não é sempre escolher um dos lados. Às vezes, a solução é combinar partes das duas versões ou escrever um novo conteúdo. A decisão precisa preservar o resultado que a equipe quer.

Ana resolve todos os trechos indicados, remove as marcações, salva os arquivos e testa a página. Depois:

```bash
git add .
git commit -m "Resolve conflito no título de contato"
git push
```

O `add` prepara os arquivos resolvidos, o `commit` conclui o merge pendente com a resolução e o `push` envia o resultado para atualizar o PR. O Git aceitar a resolução não prova que a página funciona: por isso a conferência no navegador vem antes.

Se o merge terminar automaticamente sem conflito, não há marcações para remover. Caso abra um editor para a mensagem de merge, conclua essa mensagem com orientação da pessoa instrutora. Depois, confira o resultado e envie com `git push`.

## 9. Vamos reconstruir o caminho?

Ana começa com a `main` atualizada e cria `contato`. Ela edita os arquivos, confere as mudanças, prepara com `add`, registra com `commit` e compartilha com `push`. No GitHub, abre um PR de `contato` para `main`.

A equipe revisa. Se houver pedidos de ajuste, Ana envia novos commits na mesma branch. Se houver conflito, ela combina as versões, testa e envia a resolução. Depois do merge do PR, atualiza sua `main` local.

### Perguntas para discutir antes da prática

1. Ana salvou o arquivo e executou `push`, mas não fez commit. Por que a edição não apareceu no GitHub?
2. Para que serve o `add` antes do commit?
3. Qual é a diferença entre `git checkout contato` e `git checkout -b contato`?
4. Por que trocar para `main` antes de executar `git pull origin main` neste roteiro?
5. Fazer push na `contato` coloca a tarefa na `main`?
6. O que Ana faz se receber um pedido de correção no PR aberto?
7. Quem decide o conteúdo correto quando há conflito?

### Respostas para conferir depois da conversa

1. O push envia commits; a edição salva ainda não foi registrada em um commit.
2. Selecionar o conteúdo que entrará no próximo registro.
3. O primeiro entra numa branch existente; o segundo cria uma branch e já entra nela.
4. Porque o pull integra as mudanças na branch atual, e queremos atualizar a principal local.
5. Não. A tarefa fica na branch remota `contato`; ainda precisa ser incorporada à `main`.
6. Corrige na mesma branch, salva, prepara, faz commit e push. O mesmo PR é atualizado.
7. As pessoas responsáveis pelo trabalho, considerando o resultado esperado para o projeto.
