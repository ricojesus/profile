---
description: Executa as tasks pendentes do tasks.md da feature ativa, na ordem e respeitando dependências
---

Argumento opcional (número/slug da spec, ou IDs específicos de task tipo
"T003 T004"; se vazio, usa a spec mais recente em `specs/` e todas as
tasks pendentes): $ARGUMENTS

Passos:

1. Leia `spec.md`, `plan.md` e `tasks.md` da feature alvo.
2. Monte a ordem de execução: tasks sem `[P]` são sequenciais na ordem em
   que aparecem; tasks marcadas `[P]` dentro da mesma fase podem ser
   feitas em qualquer ordem entre si, mas nunca antes de uma dependência
   explícita mencionada no texto da task.
3. Para cada task, na ordem definida:
   - Implemente exatamente o que a task descreve, no(s) arquivo(s)
     indicados.
   - Depois de implementar, marque `[x]` na linha correspondente em
     `tasks.md`.
   - Se a task depender de uma informação que só o usuário tem (dado de
     contato real, texto de uma empresa, etc.) e ela não estiver
     disponível em nenhum arquivo do repositório, pare e pergunte — não
     invente dado real de perfil profissional.
4. Nunca pule a fase de validação final do `tasks.md` (checklist de
   aceite da spec) antes de sugerir commit/push.
5. Ao final, reporte: quais tasks foram concluídas, quais ficaram
   bloqueadas (e por quê) e se o resultado está pronto para passar pelo
   checklist de `review.md`/`spec.md` antes de ir para `main`.
