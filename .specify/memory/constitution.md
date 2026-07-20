# Constituição do Projeto — Profile Website

**Versão:** 1.0.0
**Ratificada em:** 2026-07-20
**Última atualização:** 2026-07-20

Este documento define os princípios inegociáveis do projeto. Toda spec, plano
ou task gerada pelo fluxo de SDD (Spec-Driven Development) deve respeitar
estas regras. Quando um princípio for violado, a violação precisa ser
justificada explicitamente na seção "Complexity Tracking" do plano
correspondente — caso contrário o plano é rejeitado.

## Princípios

### I. Simplicidade acima de tudo
O site é HTML + CSS + JavaScript vanilla, sem build step, sem framework e
sem dependências de runtime. Qualquer proposta de introduzir bundler,
framework de UI ou gerenciador de pacotes precisa justificar por que a
simplicidade atual deixou de ser suficiente. **Por quê:** é um site de uma
página só, mantido por uma pessoa; complexidade acidental custa mais do que
resolve.

### II. Consistência de identidade
Nome, cargo e dados de contato devem ser idênticos em todos os pontos onde
aparecem: `<title>`, `<h1>`, objeto de traduções (`pageTitle`), `alt` de
imagens e rodapé. Nenhuma informação de um dono anterior do template pode
sobreviver a uma cópia/adaptação do projeto. **Por quê:** inconsistências de
nome/identidade em um site de apresentação profissional destroem a
credibilidade do visitante em segundos.

### III. Bilíngue por padrão (PT/EN)
Todo texto visível na página deve ter uma chave em `data-i18n` e uma entrada
correspondente nos dois idiomas (`pt` e `en`) dentro do objeto
`translations`. Nenhum texto novo pode ser adicionado ao HTML sem a
contraparte de tradução. **Por quê:** a alternância de idioma é uma
funcionalidade anunciada do site; meio-implementada ela vira um bug visível.

### IV. Sem dados de exemplo em produção
Nenhum deploy para produção pode conter placeholders (`Nome da Empresa`,
`Cargo / Funcao`, `seu-perfil`, `seu-usuario`, números de telefone
fictícios, etc.). Placeholders são aceitáveis apenas em specs, branches de
desenvolvimento ou preview. **Por quê:** o objetivo do site é expor o perfil
real do dono para recrutadores e clientes — placeholder no ar é pior do que
o site fora do ar.

### V. Acessibilidade e semântica mínimas
Toda imagem tem `alt` correto e descritivo (ou `alt=""` quando decorativa).
Todo controle interativo (botões de tema, idioma, voltar ao topo) tem
`aria-label` atualizado no idioma corrente. A hierarquia de headings
(`h1` → `h2` → `h3`) é respeitada. **Por quê:** é a barra mínima para um
site profissional público, e custa pouco mantê-la desde o início.

### VI. Deploy automatizado, mas nunca cego
O workflow de deploy (`.github/workflows/deploy.yml`) publica em produção a
cada push em `main`. Por isso, nenhuma alteração pode ser enviada para
`main` sem antes passar pelo checklist de revisão da spec ativa (ver
`review.md` de cada feature). Não há ambiente de staging — `main` é
produção. **Por quê:** dado o custo de errar (site público, sem
staging), a disciplina de revisão pré-push substitui a rede de segurança
que um pipeline de CI/CD mais robusto daria.

### VII. Performance e leveza
Sem fontes, ícones ou scripts de terceiros além do necessário (hoje: Google
Fonts via `preconnect`). Imagens devem ser otimizadas antes do commit. Novas
dependências externas exigem justificativa explícita no plano. **Por quê:**
tempo de carregamento é parte da primeira impressão de um site de perfil.

## Fluxo de Governança

- Esta constituição tem precedência sobre preferências individuais de
  implementação registradas em `plan.md` ou `tasks.md`.
- Alterações nesta constituição exigem incrementar a versão (semver) e
  registrar o motivo no changelog abaixo.
- Toda spec nova passa pelo fluxo `/constitution → /specify → /clarify →
  /plan → /tasks → /analyze → /implement` descrito nos comandos em
  `.claude/commands/`.

## Changelog

- **1.0.0** (2026-07-20): Versão inicial, ratificada a partir do estado
  real do código em `main` (site de perfil de Ricardo Jesus).
