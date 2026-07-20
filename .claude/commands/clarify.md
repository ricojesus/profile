---
description: Faz perguntas objetivas para resolver ambiguidades da spec ativa antes de planejar
---

Argumento opcional (número/slug da spec; se vazio, usa a spec mais
recente em `specs/`): $ARGUMENTS

Passos:

1. Identifique a spec alvo (`specs/NNN-slug/spec.md`).
2. Extraia todas as marcações `[NEEDS CLARIFICATION: ...]` do arquivo.
   Se não houver nenhuma, releia a spec procurando ambiguidades reais que
   passaram batido: requisitos vagos ("rápido", "bonito", "moderno" sem
   critério verificável), números não especificados, comportamento de
   borda não definido (ex.: o que acontece com 0 empresas cadastradas?).
3. Faça no máximo 5 perguntas por vez ao usuário (use a ferramenta de
   pergunta ao usuário, uma pergunta objetiva de cada vez ou agrupadas se
   o mecanismo permitir múltiplas de uma vez), priorizando as que mais
   afetam o `plan.md`.
4. Depois de cada resposta, edite `spec.md` imediatamente: substitua a
   marcação `[NEEDS CLARIFICATION: ...]` pelo requisito já resolvido, ou
   adicione o requisito nas seções correspondentes.
5. Nunca deixe uma resposta do usuário só na conversa — se não foi
   escrita na spec, ela vai se perder no próximo `/plan`.
6. Ao final, confirme que não restam marcações `[NEEDS CLARIFICATION]` no
   arquivo (ou liste as que ficaram pendentes por decisão do usuário de
   adiar).
