# salesforce-journey

> Documentação da minha jornada de aprendizado em Salesforce — trilha **Admin Iniciante** do Trailhead.

## Sobre este repositório

Este repositório registra minha transição de carreira para a plataforma Salesforce, iniciada em novembro de 2026 pela trilha **Admin Iniciante** do Trailhead.

Sou analista de QA com background em infraestrutura de redes e telecomunicações. O objetivo aqui não é colecionar badges, mas documentar o **raciocínio** por trás de cada decisão técnica — incluindo os erros que cometi e o que aprendi com eles.

## Contexto profissional

46 anos, formado em Redes de Computadores e em Gestão de Segurança Pública e Privada. Trajetória em infraestrutura e telecomunicações, atualmente em transição para desenvolvimento e plataformas low-code.

Trago mentalidade de testes, visão de segurança e foco em entrega.

## Trilha em andamento: Admin Iniciante

A trilha **Admin Iniciante** é o ponto de entrada para a certificação Salesforce Administrator. Cobre personalização básica da plataforma: objetos, campos, relacionamentos, automação e segurança.

<p align="center">
  <img src="imagens/img 000.png" alt="Card da trilha Admin Iniciante no Trailhead" width="600">
  <br>
  <em>Figura 1 — Trilha Admin Iniciante no Trailhead</em>
</p>

## Módulo 1: Modelagem de Dados — concluído

Módulo de 1.500 pontos dividido em três unidades. Concluí a primeira unidade (500 pontos) e sigo para as próximas.

<p align="center">
  <img src="imagens/img 001.png" alt="Tela de conclusão do desafio com +500 pontos" width="600">
  <br>
  <em>Figura 2 — Conclusão da unidade 1: +500 pontos</em>
</p>

### O que construí

- Objeto personalizado **Property** (`Property__c`) — representa um imóvel do negócio fictício DreamHouse Realty
- Campo **Price** (`Price__c`) — tipo Currency, marcado como Required
- Registro de teste: *Casa Jardim Botânico*, preço `R$ 850.000`
- Objeto personalizado **Offer** (`Offer__c`) — representa uma proposta de compra
- Campo **Offer Amount** (`Offer_Amount__c`) — tipo Currency
- Campo **Target Close Date** (`Target_Close_Date__c`) — tipo Date
- Record Name do Offer configurado como **Auto Number**, formato `OF-{0000}`
- Registro de teste: `OF-0001`, `R$ 450.000`, data alvo `15/12/2026`

### Decisões técnicas e justificativas

#### Por que Currency e não Text para preços

Escolhi o tipo **Currency** porque ele armazena o valor como número, não como texto. Isso permite somas, médias e agregações em relatórios. Um campo Text com `"850000"` seria inútil para qualquer cálculo. Além disso, o Salesforce formata automaticamente com o símbolo da moeda da organização.

#### Por que marcar Price como Required

Um imóvel sem preço é um dado incompleto. Marcar o campo como obrigatório impede que registros sejam salvos sem essa informação, garantindo integridade desde a entrada. É uma decisão de negócio traduzida em configuração.

#### Por que Auto Number no Record Name do Offer

O desafio exigia numeração automática no formato `OF-{0000}`. O ponto crítico: por padrão, o Salesforce preenche o Record Name com tipo **Text**. É preciso alterar manualmente para **Auto Number** antes de salvar. Se deixado como Text, o desafio falha.

O resultado é um identificador sequencial legível (`OF-0001`, `OF-0002`) que não depende de digitação humana.

#### Por que Date e não Date/Time

A data alvo de fechamento de uma proposta é uma data de calendário, sem hora relevante. O tipo **Date/Time** incluiria fuso horário e hora, adicionando complexidade desnecessária e risco de erro em relatórios.

### Erros cometidos e lições aprendidas

#### Erro 1: Interface em português gerou API Name incorreto

Criei o objeto com a interface do Salesforce em português. Ao digitar o rótulo "PropertyCópia" (tradução automática do Trailhead), o Salesforce gerou o API Name como `Propertyc__c` — com um "c" extra. O objeto funcionava, mas o verificador automático do Trailhead esperava `Property__c` e o desafio falhou.

**Lição:** em Salesforce, o rótulo (Label) é para humanos; o API Name é para a máquina. Nunca deixe a máquina traduzir. Configure a organização em inglês antes de começar qualquer módulo do Trailhead.

#### Erro 2: Botão "Novo" não encontrado

Perdi tempo procurando o botão "New" na tela de campos. Na interface em português ele aparece como "Criar" com menu suspenso, não como "Novo". Além disso, o botão fica no canto superior direito da tabela de campos, não no topo da página.

**Lição:** a tradução da interface quebra a correspondência com a documentação em inglês. Trabalhar em inglês elimina essa camada de tradução mental.

#### Erro 3: Aba do objeto não criada

Criei o objeto Offer sem marcar a opção *Launch New Custom Tab Wizard after saving this custom object*. O objeto existia, mas não aparecia na navegação do aplicativo. A aba não era requisito do desafio, mas impedia o teste visual do registro.

**Lição:** ao criar objetos, decida conscientemente se quer a aba. Ela pode ser criada depois em **Setup > Tabs**.

#### Erro 4: Ordem das palavras embaralhada pela tradução

A tela do desafio em português mostrava "Amount Offer" e "Target Offer Date". O enunciado original em inglês pede "Offer Amount" e "Target Close Date". Seguir a tela traduzida teria feito o desafio falhar.

**Lição:** sempre confira o enunciado original em inglês antes de nomear campos.

### Conceitos aprendidos

- **Objeto (Object):** equivalente a uma tabela de banco de dados. Contém campos (colunas) e registros (linhas).
- **Campo (Field):** atributo de um objeto. Pode ser de sistema (criado automaticamente) ou personalizado.
- **Registro (Record):** uma linha de dados dentro de um objeto.
- **Sufixo `__c`:** identifica campos e objetos personalizados (custom). Campos de sistema não têm esse sufixo.
- **Label vs API Name:** o Label é o nome exibido ao usuário e pode ser traduzido. O API Name é o identificador técnico, imutável após a criação.
- **Objetos padrão vs personalizados:** Account, Contact, Lead e Opportunity são padrão. Property e Offer são personalizados.
- **Auto Number:** tipo de campo que gera numeração sequencial automática, útil para identificadores legíveis.

### Próximos passos

1. Concluir a unidade 2 do módulo: **Criar relacionamentos de objeto** (Master-Detail e Lookup)
2. Concluir a unidade 3 do módulo
3. Avançar nos demais módulos da trilha Admin Iniciante
4. Documentar cada módulo neste repositório com o mesmo padrão: o que construí, por que decidi assim, o que errei

## Estrutura do repositório

```text
salesforce-journey/
├── README.md
├── imagens/
│   ├── img_000.png
│   └── img_001.png
└── modulos/
    └── 01-modelagem-de-dados.md
```

## Ambiente

- **Plataforma:** Salesforce Trailhead Playground (Developer Edition)
- **Org:** `cunning-badger-6gq25t-dev-ed`
- **Idioma da organização:** inglês (alterado após o Erro 1)
- **Data de início:** novembro de 2026

## Licença

Conteúdo de aprendizado pessoal. Sinta-se livre para usar como referência.# M-dulo-1-Modelagem-de-Dados_JJ
