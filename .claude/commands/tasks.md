---
description: Gera a lista de tasks (tasks.md) a partir do plan.md da spec ativa
---

Argumento opcional (número/slug da spec; se vazio, usa a spec mais
recente em `specs/`): $ARGUMENTS

Passos:

1. Leia `spec.md` e `plan.md` da feature alvo.
2. Escreva/atualize `specs/NNN-slug/tasks.md` seguindo a estrutura de
   `specs/001-perfil-profissional/tasks.md`: tasks numeradas (`T001`,
   `T002`, ...), agrupadas em fases lógicas, cada uma referenciando
   arquivo(s)/linha(s) concretos quando já existirem no código, e
   marcadas `[P]` quando puderem rodar em paralelo (arquivos diferentes,
   sem dependência entre si).
3. Toda task deve ser acionável e verificável — "implementar X" é ruim se
   X não tem critério de pronto; prefira "adicionar Y em `arquivo:linha`
   fazendo Z".
4. Inclua sempre uma fase final de validação que remete ao checklist de
   "Review & Acceptance" do `spec.md` antes de qualquer commit/push.
5. Não execute as tasks aqui — isso é papel do `/implement`.
