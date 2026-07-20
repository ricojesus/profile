---
description: Cria uma nova spec de feature em specs/NNN-slug/spec.md a partir de uma descrição em linguagem natural
---

Descrição da feature recebida do usuário: $ARGUMENTS

Se estiver vazia, pergunte ao usuário o que ele quer especificar antes de
continuar.

Passos:

1. Rode `ls specs/` para achar o maior prefixo numérico existente
   (`NNN-slug`). O novo diretório usa `NNN+1`, com um slug curto em
   kebab-case derivado da descrição (ex.: "adicionar seção de projetos"
   → `002-secao-projetos`).
2. Crie `specs/NNN-slug/spec.md` seguindo a mesma estrutura de
   `specs/001-perfil-profissional/spec.md`: Contexto, Cenários de
   usuário, Requisitos funcionais (FR-XXX, linguagem DEVE/NÃO PODE), Fora
   de escopo, Entidades-chave (se aplicável), Checklist de revisão e
   aceite.
3. Escreva a spec do ponto de vista de QUAL comportamento é esperado e
   POR QUÊ — nunca de COMO implementar (isso é papel do `/plan`). Não
   mencione tecnologias, seletores CSS ou nomes de função.
4. Marque com `[NEEDS CLARIFICATION: pergunta específica]` qualquer ponto
   em que a descrição do usuário deixou ambiguidade real (não invente
   requisito para preencher lacuna). Não adivinhe números, prazos ou
   dados de contato.
5. Confira contra `.specify/memory/constitution.md`: se a feature parecer
   violar algum princípio (ex.: pedir um framework novo, violando o
   Princípio I), avise o usuário explicitamente antes de prosseguir.
6. Ao terminar, mostre ao usuário a lista de itens `[NEEDS
   CLARIFICATION]` (se houver) e sugira rodar `/clarify` antes de
   `/plan`.
