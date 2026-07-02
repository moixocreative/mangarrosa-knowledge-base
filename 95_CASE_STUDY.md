---
project: MANGARROSA
type: case-study
status: draft
tags: [portfolio, case-study]
---

# Case Study — MANGARROSA

> Narrativa curada de portefólio. Esta é a **fonte de verdade do texto**; a publicação visual vive no projecto de portefólio, que referencia este ficheiro. Qualquer projecto — cliente, produto ou conceptual — pode activar esta camada quando se torna peça de portefólio.
>
> Manter honesto e específico: decisões concretas e resultados valem mais do que adjectivos. Os visuais são referenciados aqui, mas produzidos/publicados no portefólio.
>
> _Pré-preenchido a partir da documentação do vault (Junho 2026). Campos em itálico e `[entre parênteses]` precisam da tua validação ou de dados que só tu tens._

## Numa frase

Marketplace criativo português de dois lados que liga **Cultivadores** (criativos) a **Clientes**, assente num universo semântico próprio — o pomar — em que publicar, destacar e transaccionar têm nomes e gestos coerentes com a marca.

## Contexto e problema

O mercado criativo português vive fragmentado entre redes generalistas (onde o trabalho criativo se dilui no ruído) e plataformas internacionais (frias, caras, desenhadas para outra escala). Faltava um espaço **português, quente e específico**, onde criativos mostrem trabalho e sejam encontrados, e onde clientes lancem trabalho e contratem — sem a linguagem corporativa nem a barreira de entrada das ferramentas globais.

O problema de produto era duplo: servir **dois lados** com necessidades opostas (quem publica trabalho vs. quem procura talento) numa só plataforma coerente, e fazê-lo com uma **identidade que se destacasse** num mercado onde tudo soa igual.

_[Validar/afinar: qual foi o momento ou insight pessoal que despoletou o projecto — a tua história de origem enquanto fundador.]_

## O meu papel

**Founder & Product Designer.** Propriedade ponta-a-ponta: visão de produto, sistema de marca e nomenclatura, UX, UI, e desenvolvimento (vibe-coding com Lovable + Supabase). Projecto próprio, **real** (não conceptual).

- **Timeframe:** _[preencher — desde X até presente]_
- **Equipa:** a solo. _[mencionar colaborações pontuais, se aplicável]_
- **Stack:** React + Vite + Tailwind + Supabase, prototipado e construído via Lovable; pagamentos com Stripe.

> Nota de percurso: o projecto chamou-se **MATCHA** durante o desenvolvimento e foi renomeado **MANGARROSA**.

## Processo

### Descoberta
Definição das duas audiências (Cultivadores e Clientes) e dos seus fluxos distintos, e a decisão fundadora de construir um **universo semântico** em vez de usar linguagem genérica de marketplace. Cada acção-chave ganhou um nome do pomar: publicar é *Plantar uma Manga*, destacar é *Amadurecer*, o feed é *O Pomar*, a carteira é *A Cesta*, a moeda é a *Semente*, seguir é *Cultivar*, indicar alguém é *Polinizar*.

### Decisões-chave (e os trade-offs)

- **Moeda interna (Sementes + A Cesta) em vez de pagamento Stripe a cada transacção.** O Stripe serve só para carregar A Cesta; PRO e Amadurecer debitam da carteira (1 Semente = €1).
  _Trade-off:_ acrescenta o conceito de carteira (carga cognitiva e um passo extra), mas reduz a fricção e as taxas por micro-transacção, e abre a porta a créditos de oferta e de indicação.

- **Universo semântico próprio em vez de vocabulário genérico.**
  _Trade-off:_ marca memorável e diferenciada, ao custo de exigir alguma aprendizagem inicial ao utilizador — mitigada por copy e tooltips que ensinam o vocabulário sem atrito.

- **Regra de nomenclatura "código em inglês / UI em português".** Ficheiros, tabelas e variáveis em EN; URLs, copy e labels em PT MANGARROSA.
  _Trade-off:_ obriga a manter um mapeamento, mas garante um código universalmente legível e pronto para i18n futura.

- **Vibe-coding com Lovable para velocidade de prototipagem.**
  _Trade-off:_ iteração muito rápida do protótipo ao produto, à custa de dívida técnica — assumida e planeada para uma fase de limpeza dedicada (Fase M, pós-lançamento).

- **Experiências bloqueadas por papel (role-lock).** Criativos e Clientes vêem fluxos e funcionalidades diferentes; os Clientes usam só A Cesta, sem PRO nem indicações.
  _Trade-off:_ mais superfície de produto a manter, mas cada lado recebe exactamente o que precisa sem ruído do outro.

## Solução

Plataforma completa, com UI ponta-a-ponta sobre os dois lados:

- **O Pomar** (feed de descoberta), perfis, e **Mangas** (publicações) com destaque *Manga Madura*.
- **Chamadas** (briefs) e **Vagas** (ofertas), com fluxos de interesse e candidatura.
- **A Cesta** (carteira de Sementes), tiers **PRO**, e **Amadurecer** (destaques pagos via Cesta).
- **Polinizar** (indicações com +5 Sementes), mensagens, e camada de emails de ciclo de vida (em curso).
- Sistema de copy e nomenclatura coeso em toda a interface, no tom de voz do universo.

- **Refs visuais:** _[a produzir no projecto de portefólio — ecrãs do Pomar, fluxo de Amadurecer, carteira/Cesta, perfil de Cultivador, sistema de nomenclatura]_

## Resultado

> Estado à data: **pré-lançamento**. UI, pagamentos, indicações e copy concluídos; a fechar emails (Fase K) e QA (Fase I).

O que este projecto **demonstra**, independentemente de métricas: propriedade de produto ponta-a-ponta — sistema de marca e semântica, UX de um marketplace de dois lados, UI, desenvolvimento, integração de pagamentos e ciclo de vida de emails. Um caso onde o *design thinking* e a *execução técnica* vivem na mesma pessoa.

- **Métricas pós-lançamento (a preencher):** _[registos, activação, conversão PRO, GMV em Sementes, indicações efectivadas]_
- **Lançamento:** _[data prevista / efectiva]_

## Aprendizagens

- **O que mantinha:** o universo semântico como eixo de diferenciação — provou-se um multiplicador de identidade, não um adereço. E o modelo de carteira, que simplificou drasticamente a superfície de pagamento.
- **O que mudava:** consolidar a nomenclatura **mais cedo** (houve deriva de termos — ex. *Fruir*→*Cultivar*, *Apanhar*→*Colher* — que obrigou a auditoria posterior). E disciplinar o scope do vibe-coding para reduzir dívida técnica acumulada.
- _[Acrescentar uma aprendizagem pessoal de fundador — algo sobre decidir sozinho, priorizar, ou o salto de designer para product owner.]_

---

## Metadados de portefólio

_Para o projecto de portefólio consumir._

| Campo | Valor |
| --- | --- |
| Tipo de peça | Produto Digital |
| Real ou conceptual | Real |
| Tag de posicionamento | Product thinking · sistemas de marca · profundidade técnica · propriedade de fundador |
| Visual de capa | _[ref do portefólio]_ |
| Ordem no portefólio | _[preencher]_ |
