# Spec: Timeline de trajetória + Formação e Certificações

**Feature:** 002-timeline-formacao
**Status:** Draft
**Depende de:** [`001-perfil-profissional`](../001-perfil-profissional/spec.md)
**Input:** dados reais de carreira fornecidos pelo usuário em
2026-07-20, organizados em
[`../001-perfil-profissional/content-dados-reais.md`](../001-perfil-profissional/content-dados-reais.md).

## Contexto

A spec 001 assumiu um modelo de 3 cards curtos para "Empresas" e 4 cards
para "Serviços", preenchidos com placeholder. Os dados reais do usuário
mostram uma trajetória bem mais rica (6 posições documentadas com datas
exatas, de 2011 até hoje) e nenhum dado de "serviços" prestados — ele é
executivo de tecnologia, não presta serviços como autônomo. Esta spec
substitui esse modelo.

Decisões já validadas com o usuário (não reabrir sem motivo novo):
- A trajetória pré-2011 (5 empresas adicionais, sem data confirmada)
  **fica de fora** do site — a timeline cobre 2011–atual.
- A seção "Serviços" é **removida** e substituída por "Formação e
  Certificações".

## Cenários de usuário

### Cenário: recrutador avalia senioridade e continuidade
Um recrutador quer confirmar, em poucos segundos, que o candidato tem
trajetória contínua e ascendente em tecnologia no mercado financeiro.
Ele vê uma timeline com cargo, empresa e período de cada posição desde
2011, sem lacunas, com 3-4 conquistas quantificadas por posição.

### Cenário: visitante quer entender o "porquê" antes do "o quê"
Antes de entrar nos cards da timeline, o visitante lê um parágrafo curto
de resumo profissional (bio) que contextualiza a especialidade (mercado
financeiro, plataformas de investimento, liderança técnica).

### Cenário: verificação de credenciais
Um visitante quer confirmar formação acadêmica e certificações técnicas
relevantes (ex.: AWS) antes de prosseguir a conversa. Ele encontra uma
seção dedicada, sem precisar caçar essa informação dentro dos cards de
empresa.

## Requisitos funcionais

- **FR-101**: A hero DEVE exibir a tagline curta "Tech Manager" (mesma
  string em PT e EN — é um título de cargo, não um texto a traduzir).
- **FR-102**: Logo abaixo da hero, o site DEVE exibir uma seção "Sobre"
  com o parágrafo de resumo profissional fornecido pelo usuário,
  traduzido para EN.
- **FR-103**: A seção "Empresas" DEVE ser substituída por uma seção
  "Trajetória" (título traduzível) contendo, para cada uma das 6
  posições de `content-dados-reais.md` (Inter ×2, Espro, Rabobank ×3):
  empresa, cargo, período (mês/ano – mês/ano ou "Atual") e de 3 a 4
  bullets de destaque, em ordem cronológica decrescente (mais recente
  primeiro).
- **FR-104**: Cada posição da timeline DEVE ser visualmente distinta de
  um card de grid — layout de lista/timeline vertical, já que o volume
  de texto por item varia e não cabe bem em grid de cards de largura
  igual.
- **FR-105**: A seção "Serviços" DEVE ser removida e substituída por uma
  seção "Formação e Certificações" (título traduzível), contendo:
  - Formação acadêmica: MBA (FGV, 2016) e Bacharelado (Centro
    Universitário Ibero-Americano, 1998).
  - As 10 certificações listadas em `content-dados-reais.md`, cada uma
    com nome, instituição e ano.
- **FR-106**: Todo texto novo desta spec DEVE seguir o Princípio III da
  constituição (bilíngue por padrão) — nenhum bullet, título ou label
  pode existir só em PT.
- **FR-107**: Nenhum dado desta spec pode ser placeholder — todos os
  números e datas vêm de `content-dados-reais.md` e devem bater
  exatamente (ex.: "492 fundos", "R$ 17 bilhões", "136%").
- **FR-108** *(adendo 2026-07-20)*: A seção "Sobre" DEVE iniciar
  recolhida (3 linhas visíveis, texto cortado) com um controle "Ler
  mais"/"Read more" para expandir. O controle DEVE alternar para "Ler
  menos"/"Read less" quando expandido, expor `aria-expanded` correto e
  manter o estado (expandido/recolhido) ao trocar de idioma.

## Fora de escopo

- Carreira pré-2011 (decisão já tomada — ver Contexto).
- Links de contato reais — LinkedIn e GitHub resolvidos via T002 da spec
  001 em 2026-07-20; WhatsApp foi removido do site (deixou de ser
  requisito).
- Nova seção de "Serviços" com dado real — se no futuro o usuário passar
  a prestar serviços como autônomo, isso é uma spec `003` nova, não uma
  reintrodução desta seção.

## Entidades-chave

- **Posição** (timeline): empresa, cargo, período, lista de bullets
  (PT/EN).
- **Formação**: tipo (MBA/Bacharelado), curso, instituição, ano.
- **Certificação**: nome, instituição, ano.

## Checklist de revisão e aceite

- [ ] As 6 posições aparecem em ordem cronológica decrescente, com
      datas idênticas às de `content-dados-reais.md`.
- [ ] Nenhum bullet da timeline é uma cópia literal de todos os bullets
      do currículo formal (a spec pede curadoria de 3-4 destaques, não
      o dump completo) — a versão completa fica preservada em
      `content-dados-reais.md` como fonte.
- [ ] Seção "Serviços" não existe mais em nenhum idioma.
- [ ] Seção "Formação e Certificações" existe em PT e EN, com as 10
      certificações e as 2 formações.
- [ ] Troca de idioma/tema não deixa nenhum texto da nova seção preso no
      idioma anterior (mesma regra da spec 001, FR-007).
