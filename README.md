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
