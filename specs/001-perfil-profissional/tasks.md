# Tasks: Site de Perfil Profissional

**Feature:** 001-perfil-profissional
**Gerado a partir de:** [`plan.md`](./plan.md) + achados de
[`review.md`](./review.md)

Convenção: `[P]` = pode ser feita em paralelo com outras marcadas `[P]`
(arquivos/trechos diferentes, sem dependência). Sem `[P]` = sequencial.

## Fase 1 — Correções bloqueantes (🔴 em `review.md`)

Nenhuma delas pode ficar pendente antes do próximo push para `main`.

- [x] **T001** Corrigir `alt` da foto de perfil em `index.html:154` para
      refletir o nome real e atual do dono do site (achado 3).
- [x] **T002** LinkedIn e GitHub atualizados para os destinos reais
      (`linkedin.com/in/ricardo-oliveira-jesus`,
      `github.com/ricojesus`). Botão de WhatsApp removido por decisão do
      usuário (não é mais um requisito — ver FR-001 atualizado em
      `spec.md`).
- [x] **T003** ~~Preencher as 3 empresas...~~ **Superada** por
      [`002-timeline-formacao`](../002-timeline-formacao/tasks.md): a
      seção "Empresas" foi substituída por uma timeline de trajetória
      com 6 posições reais (2011–atual), formato bem além do que T003
      previa.
- [x] **T004** ~~Preencher os 4 serviços...~~ **Superada** por
      `002-timeline-formacao`: a seção "Serviços" foi removida (não há
      dado real de serviços prestados) e substituída por "Formação e
      Certificações".
- [x] **T005** Tradução PT/EN — feita como parte de
      `002-timeline-formacao` (todos os textos novos têm par PT/EN).

## Fase 2 — Consistência de identidade (🟡 achados 4 e 5)

- [ ] **T006** Unificar o nome em `<title>` (`index.html:6`), `<h1>`
      (`index.html:155`) e `translations.pt/en.pageTitle`
      (`index.html:30,57`) — escolher uma única forma canônica do nome e
      usá-la nos três lugares.
- [ ] **T007** Decidir explicitamente o destino da chave `pageTitle`: ou
      (a) remover, se for permanecer não usada, ou (b) ligá-la de fato —
      aplicar `document.title` dentro de `applyLanguage()`
      (`index.html:98-116`) para que a aba do navegador também traduza.
      Depende de T006.

## Fase 3 — Deploy seguro (🟡 achado 6)

- [ ] **T008** Adicionar ao workflow `.github/workflows/deploy.yml` (ou a
      um passo anterior local/CI) uma checagem simples que falha o build
      se strings de placeholder conhecidas (`Nome da Empresa`, `Nome do
      Servico`, `seu-perfil`, `seu-usuario`, `5500000000000`) ainda
      existirem em `index.html`. Não bloqueia esta spec ser fechada, mas
      deve ser aberta como spec própria se não for feita aqui.

## Fase 4 — Validação final (checklist de aceite da spec)

- [ ] **T009** Rodar manualmente o checklist de "Review & Acceptance" de
      [`spec.md`](./spec.md) contra o `index.html` resultante. Depende de
      T001–T007.
- [ ] **T010** Testar nos dois idiomas e nos dois temas (4 combinações)
      que nenhum texto placeholder ou traduzido incorretamente aparece.
      Depende de T009.
- [ ] **T011** Só então: commit + push para `main` (dispara o deploy
      automático). Depende de T010.

## Status atual

T001–T005 concluídas — nenhum bloqueante 🔴 de `review.md` continua
aberto. T006–T008 (consistência de `pageTitle` e checagem automática de
placeholder no deploy) seguem abertas, mas são 🟡, não bloqueiam push.
T009–T011 (validação final e push) ainda não foram executadas.
