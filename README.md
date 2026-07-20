# Profile Website

Site pessoal para apresentacao profissional, com foco em perfil, experiencias em empresas e servicos realizados.

## Objetivo

Este projeto foi criado para ser um site simples, clean e direto, com:

- Foto no topo
- Informacoes de contato
- Cards de empresas onde voce trabalhou
- Cards de servicos que voce realiza
- Alternancia de tema claro/escuro
- Alternancia de idioma PT/EN
- Botao de retorno ao topo

## Estrutura do projeto

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
```

## Funcionalidades

### 1) Hero

- Foto de perfil no topo
- Nome e cargo
- Botoes de contato (email, LinkedIn, GitHub e WhatsApp)

### 2) Secao de empresas

- Cards com nome da empresa, periodo, cargo e descricao

### 3) Secao de servicos

- Cards com nome do servico e descricao

### 4) Tema claro/escuro

- Botao no topo direito
- Preferencia salva no navegador (localStorage)

### 5) Traducao PT/EN

- Botao com bandeiras no topo
- Troca de textos principais da pagina
- Idioma salvo no navegador (localStorage)

### 6) Back to top

- Botao no canto inferior direito
- Aparece ao rolar a pagina
- Scroll suave para o topo

## Tecnologias

- HTML5
- CSS3
- JavaScript vanilla

## Como executar localmente

Opcao 1 (mais simples):

1. Abra o arquivo `index.html` no navegador.

Opcao 2 (servidor local):

1. No terminal, entre na pasta do projeto.
2. Execute um servidor HTTP simples, por exemplo:

```bash
python3 -m http.server 5500
```

3. Acesse no navegador:

```text
http://localhost:5500
```

## Publicacao no GitHub

Repositiorio remoto configurado:

```text
https://github.com/ricojesus/profile.git
```

Comando de push:

```bash
git push -u origin main
```

## Personalizacao rapida

No arquivo `index.html`:

- Atualize nome, cargo e links de contato
- Substitua textos dos cards de empresas e servicos

No arquivo `style.css`:

- Ajuste cores, espacamentos e tipografia

Na pasta `img/`:

- Troque `profile.jpeg` por sua foto final
- Ajuste ou substitua os arquivos de bandeira e icones

## Proximos passos sugeridos

- Adicionar projetos reais com links
- Conectar formulario de contato
- Publicar no GitHub Pages
- Melhorar SEO (meta tags e Open Graph)

## Metodologia: Spec-Driven Development (SDD)

Este projeto adota SDD: nenhuma mudanca de comportamento vai para `main`
sem antes passar por spec -> plano -> tasks -> revisao. A ideia e simples
- como o site publica direto em producao a cada push (sem staging), a
spec e o checklist de revisao fazem o papel que um ambiente de teste
faria em outro projeto.

```text
.specify/memory/constitution.md   Principios inegociaveis do projeto
specs/
  001-perfil-profissional/
    spec.md      O que o site deve fazer e por que (sem falar de "como")
    plan.md      Como implementar, respeitando a constituicao
    tasks.md     Checklist acionavel, rastreavel arquivo/linha
    review.md    Auditoria do codigo atual contra a spec
```

Fluxo para uma mudanca nova:

1. `/constitution` - so quando um principio do projeto precisa mudar.
2. `/specify` - descreve a feature em linguagem natural, gera
   `specs/NNN-slug/spec.md`.
3. `/clarify` - resolve ambiguidades antes de planejar.
4. `/plan` - gera `plan.md` (stack, arquivos afetados, trade-offs).
5. `/tasks` - quebra o plano em tasks acionaveis.
6. `/analyze` - checagem cruzada (somente leitura) entre constituicao,
   spec, plano e tasks.
7. `/implement` - executa as tasks e marca o checklist.

Esses comandos estao em `.claude/commands/` e assumem o Claude Code como
agente de execucao. O estado atual do codigo em `main` foi auditado em
[`specs/001-perfil-profissional/review.md`](specs/001-perfil-profissional/review.md)
- ha placeholders de conteudo e links que **bloqueiam** o proximo deploy
ate serem corrigidos (ver `tasks.md` da mesma pasta).
