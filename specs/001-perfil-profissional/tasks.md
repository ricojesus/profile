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
- [ ] **T002** `[P]` Substituir os placeholders de LinkedIn, GitHub e
      WhatsApp em `index.html:163,167,171` pelos destinos reais (achado 2).
- [ ] **T003** `[P]` Preencher as 3 empresas em `index.html:189-219`
      (nome, período, cargo, descrição) com dados reais, em PT.
- [ ] **T004** `[P]` Preencher os 4 serviços em `index.html:229-251`
      (nome, descrição) com dados reais, em PT.
- [ ] **T005** Replicar T003/T004 no objeto `translations.en`
      (`index.html:61-77`) — versão em inglês dos mesmos textos reais.
      Depende de T003/T004 estarem definidos primeiro (mesma fonte de
      verdade, só traduzida).

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

Nenhuma task foi concluída ainda — todos os 🔴/🟡 de `review.md` seguem
abertos no working tree em `2026-07-20`. As tasks 🟢 do review (tema,
idioma, botão voltar ao topo) não geraram tasks aqui porque já estão
conformes com a spec.
