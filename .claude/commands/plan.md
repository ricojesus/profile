---
description: Gera o plano técnico (plan.md) para a spec ativa, respeitando a constituição do projeto
---

Argumento opcional (número/slug da spec; se vazio, usa a spec mais
recente em `specs/`): $ARGUMENTS

Pré-condição: a spec alvo não deve ter marcações `[NEEDS CLARIFICATION]`
pendentes. Se tiver, pare e sugira rodar `/clarify` primeiro.

Passos:

1. Leia a spec alvo e `.specify/memory/constitution.md` por completo.
2. Escreva/atualize `specs/NNN-slug/plan.md` seguindo a estrutura de
   `specs/001-perfil-profissional/plan.md`: Resumo, Stack técnica (com
   justificativa por linha), Estrutura de arquivos afetada, Modelo de
   dados (se aplicável), decisões de UI/i18n/tema relevantes, riscos e
   decisões, e uma seção final **Complexity Tracking**.
3. Todo desvio da stack padrão do projeto (HTML/CSS/JS vanilla, sem
   build, sem dependências novas) precisa aparecer em "Complexity
   Tracking" com: o que está sendo adicionado, por que a alternativa mais
   simples não resolve, e o que fica mais simples em troca. Se não houver
   como justificar, não proponha a dependência — volte à spec e sugira
   reduzir escopo.
4. Não gere tasks aqui — isso é responsabilidade do `/tasks`.
5. Ao final, aponte explicitamente quaisquer riscos ou trade-offs que o
   usuário precisa validar antes de seguir para `/tasks`.
