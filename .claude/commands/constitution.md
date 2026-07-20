---
description: Cria ou atualiza a constituição do projeto em .specify/memory/constitution.md
---

O usuário quer criar ou atualizar a constituição do projeto. Argumentos
recebidos (podem estar vazios): $ARGUMENTS

Passos:

1. Leia `.specify/memory/constitution.md` se existir. Se não existir,
   trate como criação inicial.
2. Se o usuário deu argumentos, trate-os como os princípios/mudanças
   desejadas. Se não deu, releia o código atual do repositório (`index.html`,
   `style.css`, `README.md`, workflows em `.github/`) e proponha princípios
   consistentes com o que já existe, em vez de inventar regras genéricas.
3. Escreva/atualize `.specify/memory/constitution.md` com:
   - Lista de princípios numerados (5–9), cada um com um "Por quê" curto.
   - Seção de "Fluxo de Governança".
   - Seção de "Changelog" com versão semver e data.
4. Se já existia uma constituição, incremente a versão:
   - MAJOR: remoção/redefinição incompatível de um princípio existente.
   - MINOR: novo princípio ou expansão material de um existente.
   - PATCH: redação, esclarecimento, correção de erro, sem mudança de
     regra.
5. Depois de escrever, verifique se `spec.md`, `plan.md` ou `tasks.md` de
   specs existentes em `specs/*/` contradizem a constituição atualizada.
   Se contradizerem, liste os arquivos e as linhas afetadas para o
   usuário — não edite essas specs automaticamente.
6. Reporte ao usuário: versão antes/depois, o que mudou e quais specs
   precisam de atenção (se houver).

Nunca invente dados de contato, nomes ou métricas do projeto — se faltar
informação, pergunte em vez de assumir.
