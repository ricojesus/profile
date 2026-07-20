---
description: Faz uma checagem cruzada de consistência entre constitution, spec, plan e tasks da feature ativa (somente leitura)
---

Argumento opcional (número/slug da spec; se vazio, usa a spec mais
recente em `specs/`): $ARGUMENTS

Este comando é somente leitura — não edita nenhum arquivo. Ele só
produz um relatório.

Passos:

1. Leia `.specify/memory/constitution.md`, `spec.md`, `plan.md` e
   `tasks.md` da feature alvo.
2. Verifique e reporte:
   - **Cobertura**: todo requisito funcional (`FR-XXX`) da spec tem pelo
     menos uma task correspondente em `tasks.md`? Liste os que não têm.
   - **Duplicidade/conflito**: alguma task contradiz outra, ou o plano
     contradiz um requisito da spec?
   - **Alinhamento com a constituição**: alguma decisão do `plan.md`
     viola um princípio sem estar registrada em "Complexity Tracking"?
   - **Marcações pendentes**: restam `[NEEDS CLARIFICATION]` na spec?
   - **Terminologia**: os mesmos termos (nomes de entidades, seções) são
     usados de forma consistente nos três documentos?
3. Produza um relatório curto em formato de tabela ou lista, com
   severidade (crítico/médio/baixo) por achado, e recomende o próximo
   passo (`/clarify`, `/plan`, `/tasks` ou "pronto para `/implement`").
4. Não corrija nada automaticamente — apenas relate.
