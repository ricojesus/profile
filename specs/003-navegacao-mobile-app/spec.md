# Spec: Navegação mobile estilo app

**Feature:** 003-navegacao-mobile-app
**Status:** Implementado (2026-09-06)
**Depende de:** [`001-perfil-profissional`](../001-perfil-profissional/spec.md), [`002-timeline-formacao`](../002-timeline-formacao/spec.md)
**Input:** Issue #16 ("Estilo da versão mobile") — "Gostaria de
transformar a interface mobile em algo mais parecido com um app, onde
cada sessão será uma opção no menu, gostaria de uma barra de menu na
parte inferior da tela no estilo flutuante com cantos arredondados."
Refinado com o usuário em 2026-09-06: a navegação é por rolagem até a
seção (scroll-spy), não por troca de telas — a página continua sendo uma
rolagem única. Ainda em 2026-09-06, o usuário resolveu as duas
ambiguidades abertas: a barra substitui o botão "voltar ao topo" no
mobile, e os itens da barra usam ícone + texto.

## Contexto

O site hoje não tem nenhum menu de navegação: as quatro seções do corpo
da página (Sobre, Trajetória profissional, Projetos pessoais, Formação e
certificações) só são alcançadas rolando a página inteira. Em telas
pequenas isso torna a navegação mais cansativa do que em desktop, onde o
conteúdo é mais compacto visualmente.

O layout mobile já tem dois elementos fixos flutuantes: o botão "voltar
ao topo" (canto inferior direito, aparece só após rolar) e os botões de
tema/idioma (topo). Uma nova barra fixa na parte inferior da tela ocupa
uma região que hoje é do "voltar ao topo" — essa convivência precisa ser
decidida antes da implementação (ver Requisitos e Clarificações).

## Cenários de usuário

### Cenário principal: navegação rápida entre seções no celular
Um recrutador acessa o site pelo celular. Uma barra flutuante fixa na
parte inferior da tela, com cantos arredondados, mostra um item para
cada seção da página. Ao tocar em "Trajetória", a página rola suavemente
até o início dessa seção — sem recarregar, sem perder o tema ou o idioma
selecionados.

### Cenário: saber "onde estou" enquanto rola
Enquanto o visitante rola manualmente a página (sem usar a barra), o
item da barra correspondente à seção atualmente visível é destacado
automaticamente, funcionando como indicador de posição — não só como
atalho.

### Cenário: acessibilidade
Um visitante que navega por teclado ou leitor de tela consegue alcançar
cada item da barra de navegação, entender qual seção está selecionada no
momento (estado ativo comunicado de forma não apenas visual) e ativar o
item para mover o foco/scroll até a seção — nos dois idiomas.

### Cenário: voltar ao topo pela própria barra
Um visitante rola até o final da página no celular e quer voltar ao
início. Ele toca no item "Sobre" da barra de navegação — não existe mais
um botão "voltar ao topo" separado no mobile; a própria barra cobre essa
necessidade, já que "Sobre" é a primeira seção da página.

## Requisitos funcionais

- **FR-201**: No layout mobile, o site DEVE exibir uma barra de
  navegação fixa, flutuante, ancorada na parte inferior da tela, com
  cantos arredondados.
- **FR-202**: A barra DEVE conter exatamente um item para cada uma das
  quatro seções existentes: Sobre, Trajetória profissional, Projetos
  pessoais, Formação e certificações — nesta ordem, a mesma ordem em que
  as seções aparecem na página.
- **FR-203**: Ao ativar um item da barra (toque, clique ou teclado), a
  página DEVE rolar suavemente até o início da seção correspondente.
- **FR-204**: O item correspondente à seção atualmente visível DEVE ser
  destacado visualmente enquanto o usuário rola a página, mesmo sem
  interagir com a barra (estado ativo por posição de rolagem).
- **FR-205**: O estado ativo (FR-204) DEVE ser comunicado também a
  tecnologia assistiva (não apenas por cor/estilo visual).
- **FR-206**: A barra NÃO PODE ser exibida no layout desktop/tablet —
  fica restrita ao mesmo layout mobile que já recebe tratamento
  responsivo diferenciado no site hoje.
- **FR-207**: Todo rótulo textual da barra DEVE respeitar o idioma
  selecionado (PT/EN) e usar exatamente os mesmos nomes de seção já
  usados nos títulos (`sectionAbout`, `sectionTrajectory`,
  `sectionProjects`, `sectionFormacao`), sem mistura de idiomas
  (Princípio III da constituição).
- **FR-208**: Todo item da barra DEVE ser operável por teclado (ordem de
  foco lógica, foco visível) e ter texto acessível a leitor de tela —
  ícone sozinho, se usado, não pode ser a única forma de identificar o
  item (Princípio V da constituição).
- **FR-209**: A introdução da barra NÃO PODE remover nem quebrar
  silenciosamente as funcionalidades hoje existentes no mobile além do
  "voltar ao topo" (alternar tema, alternar idioma) — a remoção do
  "voltar ao topo" em si é intencional (ver FR-210) e não é uma
  regressão.
- **FR-210** *(resolvido em 2026-09-06)*: No layout mobile, o botão
  "voltar ao topo" hoje fixo no canto inferior direito DEVE ser removido
  e sua função absorvida pela barra de navegação: ativar o item "Sobre"
  (primeira seção da página) DEVE rolar a página de volta ao topo. O
  botão "voltar ao topo" continua existindo normalmente no layout
  desktop/tablet, onde a barra não é exibida (FR-206).
- **FR-211**: A implementação NÃO PODE introduzir framework de UI,
  bundler ou dependência de runtime nova — reaproveita HTML/CSS/JS
  vanilla já usados no site (Princípio I da constituição).
- **FR-212** *(resolvido em 2026-09-06)*: Cada item da barra DEVE exibir
  um ícone pequeno acompanhado do rótulo de texto da seção (ícone e
  texto visíveis simultaneamente — não apenas um dos dois).

## Fora de escopo

- Transformar a página numa aplicação de "uma seção por tela" (mostrar
  só a seção ativa, escondendo as demais) — descartado explicitamente
  pelo usuário em favor do scroll-spy (2026-09-06).
- Qualquer versão da barra de navegação para desktop/tablet.
- Reordenar, renomear ou remover as seções existentes — a spec assume as
  quatro seções e títulos definidos em `002-timeline-formacao`.
- Analytics de cliques nos itens do menu.

## Entidades-chave

- **Item de menu**: seção-alvo (uma das quatro seções existentes),
  rótulo (PT/EN, herdado do título da seção), ícone, estado
  (ativo/inativo).

## Checklist de revisão e aceite

- [x] Barra aparece fixa, flutuante, com cantos arredondados, apenas no
      layout mobile (FR-201, FR-206).
- [x] Os quatro itens existem, na ordem das seções, com rótulo correto
      nos dois idiomas (FR-202, FR-207).
- [x] Tocar em cada item rola até a seção correta (FR-203).
- [x] Rolar manualmente a página atualiza o item ativo sem precisar
      tocar na barra (FR-204), e o estado ativo é perceptível também via
      leitor de tela (FR-205).
- [x] Navegação completa pela barra funciona por teclado, com foco
      visível (FR-208).
- [x] Alternar tema/idioma continua funcionando igual, sem regressão
      (FR-209).
- [x] Botão "voltar ao topo" não existe mais no mobile; ativar "Sobre"
      na barra rola até o topo; no desktop/tablet o botão continua
      existindo normalmente (FR-210).
- [x] Cada item da barra mostra ícone e texto simultaneamente (FR-212).
- [x] Nenhuma dependência nova (framework, bundler, ícone de terceiros)
      foi introduzida (FR-211).

> Validado em 2026-09-06 com Playwright (Chrome do sistema) em 390×844
> (mobile) e 1440×900 (desktop), nos dois idiomas e temas — detalhes em
> [`tasks.md`](./tasks.md#status).
