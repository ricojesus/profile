# Plano Técnico: Site de Perfil Profissional

**Feature:** 001-perfil-profissional
**Spec relacionada:** [`spec.md`](./spec.md)
**Constituição:** [`.specify/memory/constitution.md`](../../.specify/memory/constitution.md)

## Resumo

Site estático de página única (SPA no sentido literal: uma única página
HTML), sem build step, hospedado como arquivos estáticos e publicado por
push direto em `main` via GitHub Actions em uma VPS própria.

## Stack técnica

| Camada       | Escolha                              | Justificativa |
|--------------|---------------------------------------|----------------|
| Marcação     | HTML5 semântico                       | Princípio I (simplicidade) |
| Estilo       | CSS3 puro, custom properties (`:root`, `[data-theme]`) | Sem necessidade de pré-processador para este volume de estilos |
| Comportamento| JavaScript vanilla, IIFE inline no `<head>`/`<body>` | Evita FOUC no tema e não exige bundler |
| Fontes       | Google Fonts (Inter), via `preconnect` | Único recurso externo permitido pelo Princípio VII |
| Ícones       | SVG inline / arquivos em `img/`       | Sem dependência de biblioteca de ícones |
| Deploy       | GitHub Actions (`appleboy/ssh-action`) → script remoto na VPS | Já implementado em `.github/workflows/deploy.yml` |

Nenhuma dependência de `npm`/`package.json` é introduzida por este plano,
em conformidade com o Princípio I.

## Estrutura de arquivos (já existente, mantida)

```text
profile/
  img/
    profile.jpeg
    br.svg
    en.svg
    back-to-top.svg
  index.html
  style.css
  README.md
  .github/workflows/deploy.yml
  .specify/                 (novo — memória da constituição)
  specs/                    (novo — specs, planos e tasks)
```

## Modelo de dados (em memória / DOM, sem backend)

- **Empresa** e **Serviço** (ver `spec.md`) são hoje hardcoded como pares
  de `<article class="card">` no HTML + chaves no objeto `translations`.
  Não há fonte de dados externa (JSON/CMS) — decisão consciente pelo
  Princípio I, dado o baixo volume de itens (3 empresas, 4 serviços).
- Se o número de cards crescer além de ~8–10, reavaliar extrair os dados
  para um array JS e gerar os cards via `template` + `render()`, mantendo
  ainda assim zero dependências externas.

## Internacionalização (PT/EN)

- Fonte da verdade: objeto `translations = { pt: {...}, en: {...} }`
  inline no `<script>` de `index.html`.
- Todo elemento traduzível carrega `data-i18n="chave"`; `applyLanguage()`
  substitui `textContent` na troca de idioma.
- Atributos que não são `textContent` (títulos `<title>`, `aria-label`,
  `alt`) precisam de tratamento explícito dentro de `applyLanguage()` —
  hoje `aria-label` dos três botões já é tratado; `<title>` e `alt` da
  foto **não são**. Isso é um gap rastreado em `review.md` e
  `tasks.md`.

## Tema claro/escuro

- Atributo `data-theme` na raiz (`<html>`), lido de `localStorage` antes
  do primeiro paint (evita flash de tema errado).
- Variáveis de cor centralizadas em `:root` e sobrescritas em
  `[data-theme="dark"]`.

## Deploy / CI

- Workflow atual dispara em todo push para `main`, conecta via SSH na VPS
  (`secrets.VPS_PROD_*`) e executa `/opt/scripts/deploy.sh
  ricardojesus.dev.br`.
- Não há passo de validação (lint de HTML, checagem de links quebrados)
  antes do deploy. Por ora isso é coberto manualmente pelo checklist de
  `spec.md` antes de mergear em `main` (Princípio VI). Automatizar essa
  checagem é candidato a uma spec futura, não faz parte deste plano.

## Riscos e decisões

- **Sem staging**: aceito conscientemente (site de baixo tráfego, deploy
  rápido de reverter via novo push). Mitigado pelo checklist pré-push.
- **Dados hardcoded no HTML**: aceito enquanto o volume de conteúdo for
  pequeno; ver seção "Modelo de dados" para o gatilho de revisão.

## Complexity Tracking

Nenhuma exceção à constituição foi necessária neste plano.
