# Plano Técnico: Timeline de trajetória + Formação e Certificações

**Feature:** 002-timeline-formacao
**Spec relacionada:** [`spec.md`](./spec.md)
**Constituição:** [`../../.specify/memory/constitution.md`](../../.specify/memory/constitution.md)

## Gatilho de complexidade (Complexity Tracking antecipado)

O `plan.md` da spec 001 previa: *"Se o número de cards crescer além de
~8–10, reavaliar extrair os dados para um array JS e gerar os cards via
`template` + `render()`, mantendo ainda assim zero dependências
externas."* Com 6 posições de timeline + 2 formações + 10 certificações
(18 itens, muitos com sub-listas de bullets), esse gatilho foi
ultrapassado. Este plano adota a extração para array JS prevista —
**sem** introduzir build step, framework ou dependência externa nova,
então não há violação do Princípio I, só o passo de escala já
antecipado.

## Modelo de dados (inline no `<script>` de `index.html`)

```js
const timeline = [
  {
    company: 'Inter',
    role: { pt: 'Sr Tech Manager', en: 'Sr Tech Manager' },
    period: { pt: 'Jul 2025 – Atual', en: 'Jul 2025 – Present' },
    bullets: {
      pt: ['...', '...', '...'],
      en: ['...', '...', '...']
    }
  },
  // ...mais 5 posições
];

const education = [
  { degree: {...}, institution: '...', year: 2016 },
  // ...
];

const certifications = [
  { name: '...', institution: '...', year: 2024 },
  // ...
];
```

- `company`, `institution` e `year` não são traduzidos (nomes próprios /
  números).
- `role`, `period` e `bullets` têm par `pt`/`en`, seguindo o mesmo
  padrão de `translations` já usado no restante do site.
- `render()` roda dentro do `DOMContentLoaded` existente, junto de
  `applyLanguage()`, e é re-executado a cada troca de idioma (mais
  simples que fazer diffing seletivo, e o volume de DOM é pequeno o
  suficiente para não haver problema de performance perceptível).

## Estrutura HTML afetada

- `<section id="empresas">` é renomeada para `<section id="trajetoria">`
  e passa a ter um `<div class="timeline">` vazio, populado via JS a
  partir de `timeline`.
- `<section id="servicos">` é removida do HTML estático e substituída
  por `<section id="formacao">`, com dois blocos: `.education-list`
  (vazio, populado a partir de `education`) e `.cert-list` (vazio,
  populado a partir de `certifications`).
- Nova `<section id="sobre">` entre a hero e `#trajetoria`, com um único
  parágrafo (`data-i18n="aboutText"`, seguindo o padrão existente de
  chave direta em `translations` — não precisa entrar no array JS por
  ser um texto único, não uma lista).
- Tagline da hero passa de `data-i18n="tagline"` com valor "IT Tech
  Manager" para valor fixo "Tech Manager" nos dois idiomas (FR-101) —
  mantém a chave `data-i18n="tagline"` por consistência de código, só
  muda o valor em `translations.pt.tagline` e `translations.en.tagline`.

## CSS novo (`style.css`)

- `.timeline`: lista vertical, item com borda esquerda/marcador,
  cabeçalho (empresa + cargo + período) e `<ul>` de bullets — layout
  substitui `.grid` dentro de `#trajetoria` (não reaproveita `.card` de
  grid, conforme FR-104).
- `.cert-list`: lista compacta (nome — instituição, ano), mais leve que
  um card por item, para não pesar visualmente com 10 entradas.
- `.education-list`: pode reaproveitar um estilo próximo ao `.card`
  existente (só 2 itens, cabe bem em cards).
- Todo CSS novo segue as mesmas custom properties já definidas em
  `:root`/`[data-theme="dark"]` — nenhuma cor nova é introduzida.

## Riscos e decisões

- **Volume de texto**: 6 posições × 3-4 bullets é bem mais conteúdo do
  que a spec 001 original previa. Mitigado por FR-103 (curadoria de 3-4
  bullets, não os 7-9 do currículo formal completo) — a versão completa
  fica em `content-dados-reais.md` como referência, não vai para o site.
- **Render via JS em vez de HTML estático**: essa é a única divergência
  do padrão anterior (empresas/serviços eram `<article>` fixos no HTML).
  Aceito porque é exatamente o gatilho de escala que o plano da spec 001
  já previu — não é um desvio não planejado.

## Complexity Tracking

Nenhuma exceção adicional à constituição — a extração para array JS já
estava prevista no plano da spec 001 como reação a crescimento de
conteúdo, não é uma dependência nova nem um framework.
