# Spec: Site de Perfil Profissional

**Feature:** 001-perfil-profissional
**Status:** Draft (retroativa — descreve o baseline já existente em `main`)
**Input:** "Site pessoal para apresentação profissional, com foco em
perfil, experiências em empresas e serviços realizados." (README.md)

## Contexto

Esta spec foi escrita retroativamente a partir do código já existente em
`index.html` / `style.css`, para servir como base do fluxo de SDD a partir
de agora. Novas mudanças no site devem ser feitas criando uma spec nova
(ex.: `002-...`) em vez de editar este arquivo diretamente — exceto
correções que fecham gaps identificados em `review.md`.

## Cenários de usuário

### Cenário principal
Um recrutador ou cliente em potencial acessa o link do site (compartilhado
via LinkedIn, currículo ou WhatsApp). Em menos de 5 segundos ele consegue
identificar: quem é a pessoa, qual o cargo/especialidade atual, como
entrar em contato, em quais empresas trabalhou e quais serviços oferece.

### Cenário: idioma
Um visitante que não lê português clica no seletor de idioma no topo e
todo o conteúdo textual da página (exceto nomes próprios) passa para
inglês, sem recarregar a página. Ao voltar depois, o idioma escolhido é
lembrado.

### Cenário: tema
Um visitante com o sistema em modo escuro abre o site à noite e prefere
não ser ofuscado por um fundo branco. Ele alterna para tema escuro pelo
botão no topo; a preferência é lembrada na próxima visita.

### Cenário: navegação em página longa
Um visitante rola a página até o final para ver todos os serviços e
depois quer voltar rapidamente ao topo sem usar o scroll manual.

## Requisitos funcionais

- **FR-001**: O site DEVE exibir, na dobra inicial (hero), foto, nome
  completo, cargo/tagline atual e botões de contato (e-mail, LinkedIn,
  GitHub). ~~WhatsApp~~ removido por decisão do usuário em 2026-07-20 —
  não é um canal de contato oferecido no site.
- **FR-002**: Todo botão de contato DEVE apontar para um destino real e
  funcional (não pode restar placeholder do tipo `seu-perfil`,
  `seu-usuario` ou número fictício).
- **FR-003**: O site DEVE ter uma seção "Empresas" com um card por empresa,
  contendo nome da empresa, período, cargo exercido e descrição das
  responsabilidades — todos com conteúdo real, não texto de exemplo.
- **FR-004**: O site DEVE ter uma seção "Serviços" com um card por serviço
  oferecido, contendo nome e descrição reais.
- **FR-005**: O site DEVE permitir alternar entre tema claro e escuro
  através de um botão fixo, com a escolha persistida em `localStorage` e
  reaplicada em visitas futuras.
- **FR-006**: O site DEVE permitir alternar entre português e inglês
  através de um botão fixo, traduzindo todo texto marcado como traduzível,
  com a escolha persistida em `localStorage`.
- **FR-007**: Todo texto visível na interface (incluindo `aria-label` dos
  três botões fixos) DEVE respeitar o idioma selecionado — não pode haver
  mistura de idiomas na mesma tela.
- **FR-008**: O `<title>` do documento, o `<h1>` visível e a entrada
  `pageTitle` do dicionário de traduções DEVEM exibir exatamente o mesmo
  nome.
- **FR-009**: Toda imagem DEVE ter um atributo `alt` correto — descritivo
  para imagens de conteúdo (ex.: foto de perfil com o nome do dono), vazio
  (`alt=""`) para imagens puramente decorativas.
- **FR-010**: O site DEVE exibir um botão "voltar ao topo" que aparece
  apenas após rolagem e realiza scroll suave até o topo ao ser clicado.
- **FR-011**: O deploy para produção (push em `main`) NÃO PODE conter
  nenhum dado de exemplo/placeholder (ver Princípio IV da constituição).

## Fora de escopo (nesta spec)

- Formulário de contato server-side.
- CMS ou painel para editar conteúdo sem mexer no HTML.
- Analytics / rastreamento de visitantes.
- Internacionalização além de PT/EN.

Esses itens aparecem no README como "Próximos passos sugeridos" e devem
virar specs próprias (`002-...`, `003-...`) quando forem priorizados.

## Entidades-chave

- **Empresa**: nome, período (texto livre "mês/ano – mês/ano"), cargo,
  descrição (PT/EN).
- **Serviço**: nome, descrição (PT/EN).
- **Contato**: tipo (email/LinkedIn/GitHub/WhatsApp), rótulo, URL/destino.

## Checklist de revisão e aceite

- [ ] Nenhum placeholder textual ou de link em `main` (FR-002, FR-003,
      FR-004, FR-011).
- [ ] Nome consistente em `<title>`, `<h1>` e `translations.pageTitle`
      (FR-008).
- [ ] Todo `alt` de imagem correto e coerente com o conteúdo atual
      (FR-009).
- [ ] Troca de idioma não deixa nenhum texto "preso" no idioma anterior
      (FR-007).
- [ ] Troca de tema e idioma persistem entre reloads (FR-005, FR-006).

> O estado atual desses itens em relação ao código em `main` está
> registrado em [`review.md`](./review.md).
