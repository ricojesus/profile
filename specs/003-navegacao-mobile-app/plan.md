# Plano Técnico: Navegação mobile estilo app

**Feature:** 003-navegacao-mobile-app
**Spec relacionada:** [`spec.md`](./spec.md)
**Constituição:** [`.specify/memory/constitution.md`](../../.specify/memory/constitution.md)

## Resumo

Adicionar uma barra de navegação fixa, flutuante, com cantos
arredondados, na parte inferior da tela — visível **apenas** no mesmo
breakpoint mobile que o site já usa (`max-width: 600px`). A barra tem 4
itens (ícone + texto), um por seção existente (Sobre, Trajetória,
Projetos, Formação), implementados como links de âncora nativos
(`<a href="#id-da-seção">`) para as seções já identificadas por `id` no
HTML atual. O destaque do item ativo durante o scroll usa
`IntersectionObserver` (API nativa do browser). O botão "voltar ao topo"
é escondido nesse mesmo breakpoint — a função é absorvida pelo item
"Sobre" da barra (FR-210).

Nenhuma dependência nova é introduzida: reaproveita CSS/JS vanilla,
variáveis de tema já existentes (`--surface`, `--border`, `--radius`) e
o mesmo objeto `translations` para os rótulos.

## Stack técnica

| Camada | Escolha | Justificativa |
|---|---|---|
| Navegação/scroll | `<a href="#secao">` nativo + `html { scroll-behavior: smooth }` (já existente) | Evita reimplementar scroll suave em JS; navegação funciona mesmo com JS desabilitado (progressive enhancement) — Princípio I |
| Estado ativo (scroll-spy) | `IntersectionObserver` nativo, um observer para as 4 `<section>` | API nativa do browser, sem polyfill necessário para o público-alvo do site; evita listener de `scroll` com cálculo manual de posição |
| Ícones | SVG inline (`stroke="currentColor"`, mesmo padrão dos ícones de contato no hero) | Consistente com o que já existe no HTML; não introduz biblioteca de ícones (Princípio VII) |
| Rótulos | Reaproveita `translations.sectionAbout` / `sectionTrajectory` / `sectionProjects` / `sectionFormacao` | Uma única fonte de verdade para o nome de cada seção (Princípio III) — a barra nunca pode dessincronizar do título da seção |
| Visibilidade mobile-only | Media query `@media (max-width: 600px)` (breakpoint já usado no site) | Não introduz um segundo breakpoint; mantém a mesma fronteira mobile/desktop que o resto do CSS responsivo |

## Estrutura de arquivos afetada

```text
profile/
  index.html   (alterado: markup da <nav> inferior + JS de render/scroll-spy)
  style.css    (alterado: .mobile-nav e itens, ajuste do .back-to-top na media query)
```

Nenhum arquivo novo de imagem/ícone — ícones são `<svg>` inline no
próprio `index.html`, ao lado da definição dos itens do menu.

## Modelo de dados (em memória / DOM, sem backend)

Um array `mobileNavItems` inline no `<script>` existente, seguindo o
mesmo padrão dos arrays já usados (`timeline`, `projects`):

```js
const mobileNavItems = [
  { sectionId: 'sobre',      i18nKey: 'sectionAbout',       icon: '<svg .../>' },
  { sectionId: 'trajetoria', i18nKey: 'sectionTrajectory',  icon: '<svg .../>' },
  { sectionId: 'projetos',   i18nKey: 'sectionProjects',    icon: '<svg .../>' },
  { sectionId: 'formacao',   i18nKey: 'sectionFormacao',    icon: '<svg .../>' }
];
```

- `sectionId` aponta para o `id` já existente de cada `<section>` — não
  cria nenhum identificador novo.
- `i18nKey` reaproveita as chaves já presentes em `translations` (sem
  duplicar string de rótulo).
- Uma função `renderMobileNav(activeLang)` monta a `<nav>` a partir desse
  array e é chamada dentro de `applyLanguage()`, no mesmo ponto onde
  `renderTimeline`/`renderProjects`/`renderFormacao` já são chamadas —
  garante que a barra também é atualizada ao trocar de idioma.

## Decisões de UI / i18n / tema

- **Estrutura semântica**: `<nav class="mobile-nav" aria-label="Navegação principal">` contendo uma lista de `<a href="#id">` — cada link tem o ícone (`aria-hidden="true"`) e o rótulo em texto visível ao lado/abaixo (atende FR-208 e FR-212: nunca só ícone).
- **Estado ativo**: um `IntersectionObserver` observa as 4 `<section>`; quando uma cruza o centro do viewport, seu item correspondente recebe uma classe `is-active` **e** `aria-current="location"` (token ARIA para "localização atual dentro da página", adequado ao scroll-spy — FR-204/FR-205). O atributo é removido dos demais itens.
- **Tema claro/escuro**: a barra usa as mesmas variáveis (`--surface`, `--border`, `--text-primary`/`--text-secondary`) já usadas em `.theme-toggle`/`.back-to-top`, então herda os dois temas automaticamente, sem CSS novo por tema.
- **"Voltar ao topo" (FR-210)**: dentro da media query mobile já existente, `.back-to-top { display: none; }` sobrepõe a regra atual — nenhuma mudança no JS de `toggleBackToTop()`/scroll listener é necessária; no desktop/tablet o botão continua funcionando exatamente como hoje.
- **Espaço para conteúdo**: a media query mobile ganha um `padding-bottom` no `main` (ou `body`) do tamanho da altura da barra, para a última seção não ficar coberta pela barra flutuante.
- **i18n**: nenhuma string nova além das 4 já existentes — não há chave de tradução a acrescentar em `translations.pt`/`translations.en`.

## Riscos e decisões

- **Ícones desenhados à mão**: como não há biblioteca de ícones, os 4 SVGs precisam ser escolhidos/desenhados com cuidado para serem reconhecíveis em tamanho pequeno (~20px). Risco de qualidade visual, não de arquitetura — mitigado revisando visualmente antes do merge (parte do checklist de `spec.md`).
- **`IntersectionObserver` com seções de altura muito diferente**: a seção "Trajetória" (quando expandida) e "Projetos" podem variar bastante de altura; o threshold do observer precisa ser calibrado (ex.: `rootMargin` centralizando uma faixa no meio do viewport) para o item ativo não "pular" de forma abrupta. Ajuste fino acontece na implementação, não muda a abordagem.
- **Hash da URL muda ao navegar**: usar `<a href="#secao">` nativo altera a URL (`/index.html#projetos`) a cada toque na barra. Não é um problema funcional (site não tem roteamento), mas é um efeito colateral visível a decidir se é aceitável — ver "Riscos a validar" abaixo.
- **Sem dependência nova**: nenhuma exceção à stack padrão foi necessária — ver Complexity Tracking.

## Complexity Tracking

Nenhuma exceção à constituição foi necessária neste plano: sem
framework, sem bundler, sem dependência de runtime nova. `IntersectionObserver`
e `<a href="#id">` são recursos nativos da plataforma web, já
equivalentes em espírito ao que o site usa hoje (`localStorage`,
`scroll-behavior: smooth`).

## Decisões validadas com o usuário (2026-09-06)

1. **URL com hash**: aceito — a URL pode ganhar `#sobre`/`#trajetoria`/
   `#projetos`/`#formacao` conforme o visitante navega pela barra. Mantém
   os links de âncora nativos, sem JS extra de scroll.
2. **Ícones**: sem referência de estilo específica — a IA escolhe
   livremente um desenho simples e coerente entre os 4 SVGs inline.
