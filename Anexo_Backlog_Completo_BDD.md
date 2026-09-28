# Anexo — Backlog Completo com Critérios de Aceitação em BDD

**Disciplina:** Macro-Módulo V — Projeto Integrador — Laboratório Ágil (LAER)
**Data de conclusão:** 28/09/2026

## Histórico do Projeto

O projeto passou por duas fases até aqui. **(1) Lean Inception:** workshop completo (Product Vision, Personas, IS/IS NOT/DOES/DOES NOT DO, Product Goals, User Journeys, Feature Brainstorming, Technical/Business/UX Review, Sequencer, MVP Canvas), que definiu o MVP. O escopo original — agendamento integrado a três serviços (banho/tosa, atendimento veterinário e hospedagem) — foi reduzido para cobrir apenas banho e tosa, registrado como Gestão de Mudança. **(2) Fase Scrum:** o MVP foi organizado em 5 Epics (E01 a E05), mapeados 1:1 às Sprints S01 a S05 seguindo a ordem de dependência técnica do Sequencer. As 15 histórias de usuário foram estimadas via Planning Poker (Fibonacci), priorizadas em MoSCoW e detalhadas com critérios de aceitação em BDD. Todo o backlog está registrado no repositório **github.com/Viniswitch/PetSlot**, com cada Epic e história como issues e sub-issues rastreáveis no Project board.

## Integrantes do Grupo

Vinicius Andrade · Thiago Alheiros · Vinicius Brito · Álvaro · João Pedro · Vicktoria

## Produto e Problema

**PetSlot** — sistema de agendamento para banho e tosa de pets. Agendamento informal (telefone, agenda física, mensagens) não considera a duração variável do atendimento por porte/pelagem do animal, nem a disponibilidade real de tosadores e boxes — gerando overbooking, atrasos em cadeia e faltas sem aviso (no-show), com impacto direto na receita e na experiência do cliente.

## Personas e Stakeholders

**Marcos (cliente):** tutor de pet que agenda banho/tosa pelo celular; quer horário rápido, sem risco de conflito.

**Atendente/gestora:** gerencia a agenda de tosadores e boxes; precisa de visão unificada e alertas de conflito.

As duas personas cobrem a totalidade dos stakeholders do projeto — não há papel externo adicional, já que os objetivos de negócio são atendidos diretamente pelos indicadores entregues à gestora.

## Product Backlog

15 histórias de usuário, cada uma com critério de aceitação em formato BDD (Given/When/Then).

### US01 - Login/Autenticação
Como **usuário (cliente ou atendente/gestora)**, quero **fazer login no sistema**, para **que meus dados e agendamentos fiquem seguros e associados à minha conta**.

```
Cenário: Login com credenciais válidas
Dado que o usuário está cadastrado no sistema
Quando ele insere usuário e senha corretos
Então o sistema libera o acesso à sua conta

Cenário: Login com credenciais inválidas
Dado que o usuário tenta fazer login
Quando ele insere credenciais incorretas
Então o sistema exibe uma mensagem de erro e não libera o acesso
```

### US02 - Cadastro de Cliente
Como **Marcos (cliente)**, quero **me cadastrar com meus dados de contato**, para **poder agendar serviços e receber notificações**.

```
Cenário: Cadastro de novo cliente
Dado que um visitante deseja se cadastrar
Quando ele preenche nome e telefone ou e-mail e confirma
Então o sistema cria a conta do cliente com sucesso

Cenário: Tentativa de cadastro duplicado
Dado que já existe um cliente cadastrado com um contato
Quando alguém tenta se cadastrar com o mesmo telefone/e-mail
Então o sistema impede o cadastro e exibe mensagem de erro
```

### US03 - Cadastro de Pets
Como **Marcos (cliente)**, quero **cadastrar meu pet com porte e tipo de pelagem**, para **que o sistema calcule automaticamente a duração do atendimento**.

```
Cenário: Cadastro de pet com dados completos
Dado que o cliente está cadastrado no sistema
Quando ele cadastra um pet informando porte e tipo de pelagem
Então o sistema salva o pet vinculado ao cliente

Cenário: Cadastro de pet com dados incompletos
Dado que o cliente está cadastrando um pet
Quando ele não informa porte ou pelagem
Então o sistema impede o cadastro e solicita as informações faltantes
```

### US04 - Cadastro de Tosadores
Como **atendente/gestora**, quero **cadastrar tosadores com suas especialidades e horários de trabalho**, para **que o sistema saiba quais profissionais estão disponíveis**.

```
Cenário: Cadastro de tosador
Dado que a atendente/gestora está cadastrando um tosador
Quando ela informa nome e horário de trabalho
Então o sistema salva o tosador com sucesso

Cenário: Agendamento fora do horário do tosador
Dado que um tosador tem horário de trabalho definido
Quando um cliente tenta agendar fora desse horário
Então o sistema impede o agendamento
```

### US05 - Perfis de Acesso
Como **atendente/gestora**, quero **que o sistema diferencie os níveis de acesso entre cliente e equipe**, para **que cada usuário só visualize e execute as ações do seu perfil**.

```
Cenário: Cliente tentando acessar tela administrativa
Dado que um cliente está autenticado no sistema
Quando ele tenta acessar uma tela administrativa
Então o sistema bloqueia o acesso

Cenário: Equipe acessando o próprio perfil
Dado que um usuário da equipe está autenticado
Quando ele acessa o sistema
Então ele visualiza as telas administrativas do seu perfil
```

### US06 - Verificação de Disponibilidade em Tempo Real
Como **Marcos (cliente)**, quero **visualizar horários disponíveis de tosadores e boxes**, para **agendar sem risco de conflito**.

```
Cenário: Exibição de horários disponíveis
Dado que um cliente está agendando um serviço
Quando ele consulta os horários disponíveis
Então o sistema exibe apenas horários com tosador e box livres simultaneamente

Cenário: Horário ocupado por outro cliente
Dado que um horário estava disponível
Quando outro cliente confirma um agendamento nesse horário primeiro
Então o sistema deixa de exibir esse horário como disponível
```

### US07 - Confirmação e Lembrete Automático
Como **Marcos (cliente)**, quero **receber confirmação e lembrete automático do meu agendamento**, para **não esquecer o horário**.

```
Cenário: Confirmação imediata
Dado que um cliente concluiu um agendamento
Quando o agendamento é confirmado pelo sistema
Então o cliente recebe uma notificação de confirmação imediatamente

Cenário: Lembrete antes do horário
Dado que um agendamento confirmado está próximo do horário marcado
Quando chega o momento definido para o lembrete
Então o sistema envia automaticamente uma notificação de lembrete
```

### US08 - Painel Geral da Agenda
Como **atendente/gestora**, quero **visualizar um painel único com a agenda de todos os tosadores e boxes**, para **não precisar cruzar informações manualmente**.

```
Cenário: Visualização consolidada da agenda
Dado que a atendente/gestora acessa o painel de agenda
Quando ela seleciona um dia ou uma semana
Então o sistema exibe todos os agendamentos de todos os tosadores e boxes nesse período
```

### US09 - Indicadores de Ocupação e No-show
Como **atendente/gestora**, quero **acompanhar indicadores de ocupação e taxa de no-show**, para **avaliar o desempenho da operação**.

```
Cenário: Exibição dos indicadores
Dado que existem agendamentos registrados no sistema
Quando a atendente/gestora acessa o painel de indicadores
Então o sistema exibe a taxa de ocupação e a taxa de no-show calculadas automaticamente

Cenário: Filtro por período
Dado que a atendente/gestora está no painel de indicadores
Quando ela seleciona um dia ou semana específica
Então o sistema recalcula os indicadores para o período selecionado
```

### US10 - Cadastro de Boxes
Como **atendente/gestora**, quero **cadastrar os boxes disponíveis**, para **que o sistema saiba quantos recursos físicos existem para alocar**.

```
Cenário: Cadastro de novo box
Dado que a atendente/gestora está cadastrando boxes
Quando ela informa a identificação de um novo box
Então o sistema salva o box como recurso disponível

Cenário: Bloqueio de box já ocupado
Dado que um box já está reservado em um horário
Quando um novo agendamento tenta usar o mesmo box no mesmo horário
Então o sistema impede o agendamento simultâneo
```

### US11 - Cálculo Automático de Duração
Como **Marcos (cliente)**, quero **que o sistema calcule automaticamente a duração do atendimento pelo porte/pelagem do pet**, para **que o horário reservado seja realista**.

```
Cenário: Cálculo de duração pelo perfil do pet
Dado que um pet está cadastrado com porte e pelagem definidos
Quando um cliente inicia um agendamento para esse pet
Então o sistema calcula automaticamente a duração do atendimento com base nessas características
```

### US12 - Agendamento Online
Como **Marcos (cliente)**, quero **agendar um horário de banho e tosa direto pelo sistema**, para **não precisar ligar ou mandar mensagem**.

```
Cenário: Confirmação de agendamento válido
Dado que um cliente selecionou um horário disponível
Quando ele confirma o agendamento
Então o sistema registra a reserva vinculando cliente, pet, tosador e box

Cenário: Tentativa de agendamento em horário indisponível
Dado que um cliente está confirmando um agendamento
Quando o tosador ou box selecionado deixou de estar disponível
Então o sistema recusa o agendamento e informa a indisponibilidade
```

### US13 - Bloqueio Anti-Overbooking
Como **atendente/gestora**, quero **que o sistema impeça agendamentos sem recurso disponível**, para **que não ocorra overbooking**.

```
Cenário: Rejeição de agendamento conflitante
Dado que um tosador ou box já está reservado em um horário
Quando um novo agendamento tenta usar o mesmo recurso no mesmo horário
Então o sistema rejeita o agendamento
```

### US14 - Alertas de Conflito
Como **atendente/gestora**, quero **receber um alerta quando houver conflito de horário**, para **resolver antes do atendimento**.

```
Cenário: Alerta de conflito detectado
Dado que existem dois agendamentos usando o mesmo recurso no mesmo horário
Quando o sistema detecta essa sobreposição
Então ele exibe um alerta no painel da atendente/gestora indicando o recurso afetado
```

### US15 - Reagendamento e Cancelamento pelo Cliente
Como **Marcos (cliente)**, quero **reagendar ou cancelar meu horário pelo sistema**, para **não precisar ligar quando meus planos mudarem**.

```
Cenário: Cancelamento libera o horário
Dado que um cliente possui um agendamento confirmado
Quando ele solicita o cancelamento
Então o sistema libera automaticamente o horário para outro cliente

Cenário: Reagendamento segue as regras de disponibilidade
Dado que um cliente possui um agendamento confirmado
Quando ele solicita reagendamento para um novo horário
Então o sistema aplica as mesmas regras de disponibilidade e bloqueio anti-overbooking do agendamento original
```

## Priorização (MoSCoW)

| # | História | Prioridade |
|---|---|---|
| US01 | Login/Autenticação | Must have |
| US02 | Cadastro de Cliente | Must have |
| US03 | Cadastro de Pets | Must have |
| US04 | Cadastro de Tosadores | Must have |
| US10 | Cadastro de Boxes | Must have |
| US11 | Cálculo Automático de Duração | Must have |
| US06 | Verificação de Disponibilidade em Tempo Real | Must have |
| US12 | Agendamento Online | Must have |
| US13 | Bloqueio Anti-Overbooking | Must have |
| US05 | Perfis de Acesso | Should have |
| US07 | Confirmação e Lembrete Automático | Should have |
| US08 | Painel Geral da Agenda | Could have |
| US09 | Indicadores de Ocupação e No-show | Could have |
| US14 | Alertas de Conflito | Could have |
| US15 | Reagendamento e Cancelamento | Won't have (this time) |

*Conferência: Must ≈ 62% do esforço total (em pontos) — dentro do razoável (~60%), a priorização não ficou "achatada".*

## Justificativa Técnica das Decisões

O escopo original (agendamento integrado a três serviços — banho/tosa, veterinário e hospedagem) foi reduzido para cobrir apenas banho e tosa, evitando a complexidade de modelar conflitos entre categorias de recursos distintas sem alterar a natureza do problema central (overbooking e no-show por falta de controle de disponibilidade).

As duas personas definidas cobrem os dois lados de qualquer transação do sistema — quem consome o serviço e quem o opera — e por isso também representam a totalidade dos stakeholders; não há papel adicional cujos interesses divirjam dos dessas personas dentro do escopo definido.

O backlog passou por três filtros sucessivos antes da priorização final: (1) um Lean Inception gerou a lista bruta de funcionalidades e uma triagem por esforço técnico × valor de negócio × valor de UX, já descartando itens de alto custo e baixo retorno para o backlog futuro; (2) um Sequencer organizou o que restou em ondas de dependência técnica; (3) essa mesma ordem foi reclassificada em MoSCoW — a base técnica e o fluxo de agendamento formam o Must have (nada posterior funciona sem eles), perfis de acesso e notificações formam o Should have, painel e indicadores formam o Could have, e reagendamento ficou como Won't have nesta versão, coerente com a redução de escopo já decidida.

Essa cadeia — problema → escopo → personas → features → matriz Effort×Business×UX → Sequencer → MoSCoW — mantém rastreabilidade: cada história do Must have é justificável tanto por dependência técnica quanto por valor de negócio, e nenhuma prioridade contradiz os objetivos definidos (reduzir no-show, aumentar ocupação, aumentar retenção).
