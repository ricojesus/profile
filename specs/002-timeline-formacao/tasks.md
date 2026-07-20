# Tasks: Timeline de trajetória + Formação e Certificações

**Feature:** 002-timeline-formacao
**Gerado a partir de:** [`plan.md`](./plan.md)

## Fase 1 — Conteúdo

- [x] **T101** Curar 3-4 bullets de destaque por posição (das 6) a
      partir dos bullets completos em
      `../001-perfil-profissional/content-dados-reais.md`, em PT.
- [x] **T102** Traduzir para EN: bio (Sobre), tagline, os bullets
      curados de T101, formação e certificações (nomes de
      instituição/certificação não se traduzem).

## Fase 2 — Estrutura (`index.html`)

- [x] **T103** Adicionar `timeline`, `education`, `certifications` como
      arrays JS dentro do `<script>` existente, com os dois idiomas
      (T101/T102). Depende de T101, T102.
- [x] **T104** Adicionar seção `#sobre` (bio) entre a hero e
      `#trajetoria`, com `data-i18n="aboutText"` e entrada em
      `translations.pt/en`.
- [x] **T105** Renomear `#empresas` para `#trajetoria`, remover os 3
      `<article class="card">` estáticos, adicionar `<div
      class="timeline"></div>` vazio.
- [x] **T106** Remover `#servicos` por completo (os 4 `<article
      class="service-card">` e as chaves `serviceName*`/`serviceDesc*`
      de `translations`).
- [x] **T107** Adicionar `#formacao` com `.education-list` e
      `.cert-list` vazios, no lugar de onde `#servicos` estava.
- [x] **T108** Escrever função `renderTimeline()` /
      `renderFormacao()` que lê os arrays de T103 e popula o DOM,
      chamada dentro de `applyLanguage()` (para re-renderizar ao trocar
      idioma). Depende de T103–T107.
- [x] **T109** Atualizar `translations.pt.tagline` e
      `translations.en.tagline` para `"Tech Manager"` (mesma string nos
      dois idiomas, FR-101).

## Fase 3 — Estilo (`style.css`)

- [x] **T110** `[P]` Estilo `.timeline` e item de timeline (marcador,
      cabeçalho empresa/cargo/período, lista de bullets).
- [x] **T111** `[P]` Estilo `.cert-list` (lista compacta).
- [x] **T112** `[P]` Estilo `.education-list` (2 itens, pode reusar
      aparência próxima de `.card`).
- [x] **T113** Responsivo: conferir os três estilos acima em
      `@media (max-width: 600px)`. Depende de T110–T112.

## Fase 4 — Validação

- [x] **T114** Testar nos dois idiomas × dois temas (4 combinações): a
      timeline, a bio e a formação/certificações renderizam
      corretamente, sem texto preso no idioma anterior. Depende de
      T108, T109, T113.
- [x] **T115** Rodar o checklist de "Review & Acceptance" de
      [`spec.md`](./spec.md). Depende de T114.
- [x] **T116** Atualizar `tasks.md` da spec 001 (marcar T003/T004 como
      resolvidas por esta spec, ou substituídas). Depende de T115.

## Fase 5 — Adendo 2026-07-20 (FR-108)

- [x] **T117** Seção "Sobre" recolhida por padrão (3 linhas, CSS
      `-webkit-line-clamp`), botão "Ler mais"/"Ler menos" com
      `aria-expanded`, estado preservado ao trocar idioma.
- [x] **T118** Atualizar links de contato: LinkedIn e GitHub reais;
      remover botão de WhatsApp (deixou de ser requisito, T002 da spec
      001 fechado).

## Fase 6 — Adendo 2026-07-20 (FR-109, FR-110)

- [x] **T119** Adicionar campo `logo` a cada posição da timeline
      (`img/inter.png`, `img/espro.jpg`, `img/rabobank.png`,
      `img/cmcapital.jpg`) e renderizar em badge de fundo branco fixo
      (`.timeline-logo`), `alt=""`.
- [x] **T120** Adicionar posição "CM Capital Markets — Coordenador de
      Sistemas" (Dez 2006 – Jun 2011) ao array `timeline`, com 4
      bullets PT/EN curados a partir do relato formal do usuário.
      Depende de T119.
- [x] **T121** Confirmar que a Mambu fica de fora por ora (decisão
      explícita do usuário) — arquivo `img/mambu.webp` mantido no
      repositório sem uso, documentado em `content-dados-reais.md`.
- [x] **T122** Botão "Ver trajetória completa" (`.section-toggle`),
      recolhendo `#timelineList` por padrão (`.timeline.is-hidden`),
      com `aria-expanded`/`aria-controls` e label traduzido que
      preserva estado ao trocar idioma (mesmo padrão de T117).

- [x] **T123** Seção "Projetos Pessoais" (`#projetos`) criada entre
      `#trajetoria` e `#formacao`, com array `projects` (mesmo padrão
      `render*()` dos demais dados) e primeiro item: Gold Virtual
      Airlines — Portal Administrativo, PHP 7, PT/EN. Sem link (não
      fornecido pelo usuário) — fácil adicionar depois se surgir um.
      Validado com `node --check`, jsdom (ordem das seções e conteúdo
      PT/EN) e screenshot real claro/escuro via Playwright.
- [x] **T124** Logo do projeto (`img/gold.jpg`) adicionado ao card em
      badge branco (`.project-logo`), mesmo tratamento visual do logo
      de empresa na timeline (FR-109). Validado visualmente claro/
      escuro.
- [x] **T125** Campo `since` ("Em produção desde 2018"/"In production
      since 2018") adicionado ao card, como terceira linha abaixo do
      papel/descritor. Validado PT/EN e visualmente.
- [x] **T126** Segundo card: Gold Acars (C#, WPF, PHP Laravel, FSUIPC),
      em produção desde 2020, reaproveitando o logo `img/gold.jpg`
      (mesma marca, sem logo próprio enviado). Validado: 2 cards lado a
      lado, 4 stack tags, PT/EN, claro/escuro.
- [x] **T127** Ajuste de header: os dois cards passam a usar `name`
      "Gold Virtual Airlines" (a marca) e `role` como o nome do sistema
      específico ("Portal Administrativo" / "Gold Acars"), removendo o
      texto "Coletor de Telemetria". Validado via jsdom (h3/role de
      cada card) e screenshot.

## Observação

WhatsApp foi removido do site por decisão do usuário — não é mais uma
pendência.

## Status

Todas as tasks concluídas em 2026-07-20. Validação (T114) feita com:
JS checado com `node --check`; DOM renderizado via jsdom para conferir
os 6 itens de timeline, 2 formações e 10 certificações em PT e EN;
screenshots reais via Playwright/Chromium (claro/PT, escuro/PT,
escuro/EN) servindo `index.html` em `python3 -m http.server` — layout
correto nas 4 combinações, sem placeholder residual, sem erros de
console no reload. Ferramentas de teste instaladas só no diretório de
scratchpad da sessão, não no projeto.
