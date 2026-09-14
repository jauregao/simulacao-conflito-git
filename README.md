# Simulação de conflito no Git

Este repositório foi preparado para uma demonstração em aula. Duas pessoas alteraram o mesmo título da seção de contato de formas diferentes:

- a branch `main` contém a mudança feita por Bruno;
- a branch `ana-contato` contém a mudança feita por Ana.

Na cópia preparada no computador da pessoa instrutora, o repositório começa na branch `ana-contato`, antes da tentativa de juntar as alterações.

Se você clonou este repositório pelo GitHub, ele será aberto inicialmente na `main`. Prepare a demonstração com:

```bash
git checkout ana-contato
```

O comando troca para a branch de Ana. Confirme com `git status` que não há mudanças pendentes antes de continuar.

Durante a demonstração, o conflito será provocado com:

```bash
git merge main
```

Depois, a turma deverá decidir qual título ficará no `index.html`, apagar as marcações criadas pelo Git, salvar o arquivo e concluir a resolução.
