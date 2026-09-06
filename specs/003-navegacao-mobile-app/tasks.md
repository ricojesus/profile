# Tasks: Navegação mobile estilo app

**Feature:** 003-navegacao-mobile-app
**Gerado a partir de:** [`plan.md`](./plan.md)

## Fase 1 — Ícones e dados (`index.html`)

- [x] **T301** Desenhar/escolher 4 ícones SVG inline simples (24×24,
      `stroke="currentColor"`, sem preenchimento sólido — mesmo estilo
      dos ícones de contato do hero em `index.html:465-475`), um para
      cada seção: Sobre (ex.: usuário/perfil), Trajetória (ex.:
      maleta/linha do tempo), Projetos (ex.: pasta/código), Formação
      (ex.: capelo/diploma).
- [x] **T302** Adicionar o array `mobileNavItems` no `<script>`
      existente (perto dos arrays `timeline`/`projects`/`education`,
      após `index.html:258`), com `sectionId`, `i18nKey` e o `icon` de
      T301 para as 4 seções (`sobre`, `trajetoria`, `projetos`,
      `formacao`), na mesma ordem em que aparecem na página. Depende de
      T301.

## Fase 2 — Estrutura e comportamento (`index.html`)

- [x] **T303** Escrever `renderMobileNav(activeLang)` — monta a `<nav
      class="mobile-nav" aria-label="Navegação principal">` a partir de
      `mobileNavItems`, um `<a href="#sectionId">` por item com o SVG
      (`aria-hidden="true"`) e um `<span>` com o rótulo traduzido
      (`translations[activeLang][item.i18nKey]`). Segue o mesmo padrão
      de `renderTimeline`/`renderProjects` (`index.html:293-344`).
      Depende de T302.
- [x] **T304** Chamar `renderMobileNav(activeLang)` dentro de
      `applyLanguage()` (`index.html:391-393`, junto das outras
      chamadas `render*`), para a barra atualizar o rótulo ao trocar de
      idioma. Depende de T303.
- [x] **T305** Adicionar o placeholder `<div id="mobileNav"></div>` (ou
      elemento equivalente) no HTML, fora de `<main>`, ao lado de
      `#backToTop` (`index.html:19-21`), para `renderMobileNav`
      preencher.
- [x] **T306** Implementar o scroll-spy: um `IntersectionObserver`
      observando as 4 `<section>` (`index.html:501,508,515,521`);
      no callback, adicionar `class="is-active"` +
      `aria-current="location"` ao `<a>` da seção mais visível em
      `#mobileNav` e remover dos demais. Registrar o observer dentro do
      `document.addEventListener('DOMContentLoaded', ...)` existente
      (`index.html:274`), depois da primeira chamada de
      `applyLanguage()`. Depende de T303, T305.

## Fase 3 — Estilo (`style.css`)

- [x] **T307** `[P]` Estilo base de `.mobile-nav` — `position: fixed`,
      ancorada na parte inferior central, cantos arredondados, usando
      `--surface`/`--border`/`box-shadow` no mesmo padrão de
      `.back-to-top` (`style.css:562-597`); **escondida por padrão**
      (só aparece dentro da media query mobile, T309).
- [x] **T308** `[P]` Estilo dos itens (`.mobile-nav a`): ícone + rótulo
      empilhados, área de toque confortável (mín. ~44px), cor
      `--text-secondary` no estado normal e `--accent`/`--text-primary`
      quando `.is-active`/`aria-current="location"`.
- [x] **T309** Dentro de `@media (max-width: 600px)`
      (`style.css:600-657`): exibir `.mobile-nav` (`display: flex`),
      esconder `.back-to-top` (`display: none`, resolvendo FR-210), e
      adicionar `padding-bottom` em `main` do tamanho da altura da
      barra para o conteúdo da última seção não ficar coberto. Depende
      de T307, T308.

## Fase 4 — Validação

- [x] **T310** Testar nos dois idiomas × dois temas (4 combinações) no
      viewport mobile: os 4 itens aparecem com rótulo e ícone corretos,
      tocar em cada um rola até a seção certa, o item ativo muda
      conforme o scroll manual. Depende de T304, T306, T309.
- [x] **T311** Testar em viewport desktop/tablet (>600px): `.mobile-nav`
      não aparece, `.back-to-top` continua funcionando exatamente como
      antes (sem regressão — FR-209). Depende de T309.
- [x] **T312** Testar navegação por teclado (Tab entre os 4 itens, Enter
      ativa) e conferir com leitor de tela/inspeção de acessibilidade
      que o rótulo de texto é lido (não só o ícone) e que o item ativo é
      identificável via `aria-current` (FR-205, FR-208). Depende de
      T306.
- [x] **T313** Rodar o checklist de "Review & Acceptance" de
      [`spec.md`](./spec.md). Depende de T310, T311, T312.

## Status

Todas as tasks concluídas em 2026-09-06. Validação (T310–T312) feita
com Playwright (canal `chrome`, apontando para o Google Chrome já
instalado, já que o Chromium embutido do Playwright não suporta esta
versão do macOS): screenshots reais em mobile (390×844, PT/claro,
PT/escuro→click, EN/escuro) e desktop (1440×900); JS avaliado no
contexto da página para conferir `display` computado, ordem/rótulo dos
4 itens, `aria-current="location"` após clique, atualização do item
ativo por scroll manual (sem clique) e navegação por teclado
(Tab + Enter ativando o link). Único erro de console observado foi
404 de `favicon.ico` do servidor de teste (`python3 -m http.server`),
sem relação com a implementação. Ferramentas de teste (Playwright)
instaladas só no diretório de scratchpad da sessão, não no projeto.
