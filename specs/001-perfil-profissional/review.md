# Revisão: estado atual do código vs. spec 001

**Data:** 2026-07-20
**Revisado contra:** `index.html` (working tree, incluindo a mudança de
título ainda não commitada), `style.css`, `.github/workflows/deploy.yml`

Legenda: 🔴 bloqueia deploy em produção (viola Princípio IV ou II) · 🟡
inconsistência/gap menor · 🟢 conforme.

> **Atualização 2026-07-20 (mesmo dia):** achado 1 resolvido pela spec
> [`002-timeline-formacao`](../002-timeline-formacao/spec.md) — conteúdo
> real substituiu os placeholders de empresas/serviços. Achado 2 (links
> de contato) segue em aberto. Ver
> [`../001-perfil-profissional/tasks.md`](./tasks.md) para status
> atualizado por task.

## Achados

### 🔴 1. Conteúdo de empresas e serviços é 100% placeholder — ✅ resolvido
`index.html:189-251` — as três empresas e os quatro serviços ainda usam
literalmente o texto de exemplo do template: "Nome da Empresa", "Cargo /
Funcao", "Nome do Servico", "Descricao do servico oferecido...". As chaves
equivalentes em `translations` (linhas 34-50 e 61-77) repetem o mesmo
texto genérico em PT e EN.
**Viola:** FR-003, FR-004, Princípio IV.
**Impacto:** se isso for publicado como está, o site mostra um currículo
vazio — pior do que não ter site.

### 🔴 2. Links de contato são placeholders — ✅ resolvido
LinkedIn e GitHub atualizados para os destinos reais em 2026-07-20; o
botão de WhatsApp foi removido por decisão do usuário (deixou de ser
requisito, ver FR-001 atualizado em `spec.md`).
**Violava:** FR-002.

### 🔴 3. `alt` da foto de perfil está com o nome errado
`index.html:154` — `<img src="img/profile.jpeg" alt="Lucilene de Jesus" ...>`.
O `<title>` (linha 6) e o `<h1>` (linha 155) já foram atualizados para
"Ricardo Oliveira de Jesus" / "Ricardo Jesus", mas o `alt` da foto ainda
tem o nome do dono anterior do template.
**Viola:** FR-008, FR-009, Princípio II. Este é o achado mais grave do
ponto de vista de credibilidade: é o tipo de detalhe que um visitante
atento (ex.: recrutador técnico inspecionando o HTML) percebe na hora.

### 🟡 4. Três versões diferentes do nome coexistindo
- `<title>`: "Ricardo Oliveira de Jesus" (`index.html:6`)
- `<h1>`: "Ricardo Jesus" (`index.html:155`)
- `translations.pt/en.pageTitle`: "Ricardo Jesus" (`index.html:30,57`)

`pageTitle` nunca é lido em lugar nenhum do código — não há elemento com
`data-i18n="pageTitle"` nem atribuição a `document.title` dentro de
`applyLanguage()`. É uma chave morta hoje, mas o valor diverge do
`<title>` real, então se algum dia for ligada, vai propagar a
inconsistência.
**Viola:** FR-008.

### 🟡 5. `<title>` não muda com o idioma
Mesmo que `pageTitle` fosse aplicada, hoje `applyLanguage()`
(`index.html:98-116`) nunca toca `document.title`. Não é um requisito
crítico, mas está implícito em FR-006 ("todo texto visível... incluindo o
que aparece na aba do navegador" é uma leitura razoável) e é inconsistente
com o cuidado dado ao resto da i18n.

### 🟡 6. Deploy sem validação antes de ir para produção
`.github/workflows/deploy.yml` dispara em todo push para `main` e não
roda nenhuma checagem (lint de HTML, link-check, ou ao menos um `grep`
atrás de placeholders conhecidos) antes de rodar o script de deploy na
VPS. Combinado com os achados 1–3, isso significa que o estado atual do
working tree, se commitado e enviado, iria ao ar com dados fictícios.
**Viola:** Princípio VI (o checklist pré-push é hoje 100% manual e,
pelos achados acima, não está sendo seguido).

### 🟢 7. Tema claro/escuro
Implementação em `index.html:24-26,93-96,129-135` e `style.css:7-25` está
completa e consistente com FR-005: leitura de `localStorage` antes do
primeiro paint (evita flash), toggle funcional, ícone atualizado.

### 🟢 8. Alternância de idioma (mecanismo)
O mecanismo em si (`applyLanguage`, `data-i18n`, persistência em
`localStorage`) está correto e cobre `aria-label`/`title` dos botões
fixos — só falha nos pontos específicos já listados (achados 4 e 5).

### 🟢 9. Botão "voltar ao topo"
`index.html:118-124,143-147` + `style.css:283-318` — aparece após 280px
de scroll, some no topo, scroll suave. Conforme FR-010.

### 🟢 10. `.gitignore` / `.DS_Store`
Arquivos `.DS_Store` existem no working tree mas não estão rastreados
pelo git — `.gitignore` já cobre isso corretamente.

## Resumo por requisito da spec

| Requisito | Status |
|-----------|--------|
| FR-001 (hero completo) | 🟡 estrutura ok, conteúdo de contato parcialmente placeholder |
| FR-002 (links reais) | 🟢 atendido |
| FR-003 (empresas reais) | 🟢 atendido — via `002-timeline-formacao` (trajetória substitui empresas) |
| FR-004 (serviços reais) | 🟢 n/a — seção removida por decisão do usuário, ver `002-timeline-formacao` |
| FR-005 (tema persistente) | 🟢 atendido |
| FR-006 (idioma persistente) | 🟢 atendido |
| FR-007 (sem mistura de idioma) | 🟢 atendido |
| FR-008 (nome consistente) | 🔴 não atendido |
| FR-009 (alt correto) | 🟢 atendido (achado 3 resolvido, ver T001) |
| FR-010 (voltar ao topo) | 🟢 atendido |
| FR-011 (sem placeholder em produção) | 🟢 atendido — nenhum achado 🔴 pendente |

## Recomendação

Atualização 2026-07-20: os três achados bloqueantes (🔴 1, 2 e 3) foram
resolvidos. Restam apenas os 🟡 (T006–T008 em `tasks.md`), que não
impedem publicar. Antes do próximo push, ainda falta rodar a validação
final (T009–T010 em `tasks.md`).
