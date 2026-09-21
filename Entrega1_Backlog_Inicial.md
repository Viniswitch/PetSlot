# Entrega 1 — Backlog Inicial

**Disciplina:** Macro-Módulo V — Projeto Integrador — Laboratório Ágil (LAER)
**Data de conclusão:** 28/09/2026

---

## Integrantes do Grupo

- Vinicius Andrade
- Thiago Alheiros
- Vinicius Brito
- Álvaro

---

## Produto e Problema

**Produto:** PetSlot — sistema de agendamento para banho e tosa de pets.

**Problema:** Agendamento informal (telefone, agenda física, mensagens) não considera a duração variável do atendimento por porte/pelagem do animal, nem a disponibilidade real de tosadores e boxes — gerando overbooking, atrasos em cadeia e faltas sem aviso (no-show), com impacto direto na receita e na experiência do cliente.

---

## Personas e Stakeholders

As duas personas identificadas cobrem integralmente os interessados no sistema — não há stakeholder externo adicional (ex.: dono de negócio), já que os objetivos de gestão (Product Goals) são atendidos diretamente pelos indicadores entregues à atendente/gestora.

**Persona 1 — Marcos (cliente)**
- Perfil: tutor de pet, agenda banho/tosa com frequência, resolve tudo pelo celular
- Comportamento: prefere app/mensagem a ligação
- Necessidades: marcar horário rápido, sem risco de conflito

**Persona 2 — Atendente/gestora**
- Perfil: responsável por gerenciar a agenda de tosadores e boxes
- Comportamento: acessa o sistema várias vezes ao dia, precisa de alertas de conflito
- Necessidades: visão clara de disponibilidade, sem cruzar informações manualmente

---

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

---

## Priorização (MoSCoW)

| História | Categoria |
|---|---|
| US01 — Login/Autenticação | Must have |
| US02 — Cadastro de Cliente | Must have |
| US03 — Cadastro de Pets | Must have |
| US04 — Cadastro de Tosadores | Must have |
| US10 — Cadastro de Boxes | Must have |
| US11 — Cálculo automático de duração | Must have |
| US06 — Verificação de disponibilidade em tempo real | Must have |
| US12 — Agendamento online | Must have |
| US13 — Bloqueio anti-overbooking | Must have |
| US05 — Perfis de Acesso | Should have |
| US07 — Confirmação/lembrete automático | Should have |
| US08 — Painel geral da agenda | Could have |
| US09 — Indicadores de ocupação/no-show | Could have |
| US14 — Alertas de conflito | Could have |
| US15 — Reagendamento/cancelamento | Won't have (this time) |

*Conferência: Must = 29 pts, Should = 8 pts, Could = 10 pts (excluindo Won't) → Must representa ~62% do esforço total — dentro do razoável (~60%), a priorização não ficou "achatada".*

---

## Justificativa Técnica das Decisões

**Escopo e problema.** O projeto partiu de um requisito mais amplo — agendamento integrado para três serviços (banho/tosa, atendimento veterinário e hospedagem) — reduzido ainda na fase de definição para cobrir apenas banho e tosa. Essa decisão foi técnica, não arbitrária: um agendamento com três serviços exigiria modelar conflitos de recursos entre categorias distintas (sala de atendimento veterinário, box de tosa, vaga de hospedagem), triplicando a complexidade de regras de negócio sem que o núcleo do problema — overbooking e no-show por falta de controle de disponibilidade — mudasse de natureza. Reduzir o escopo manteve o problema central intacto e viabilizou entregar um MVP coerente dentro do prazo da disciplina.

**Personas e stakeholders.** Foram definidas duas personas: Marcos (cliente, que agenda o serviço) e a atendente/gestora (equipe interna, que opera a agenda). Essas duas cobrem integralmente os dois lados de qualquer transação do sistema — quem consome o serviço e quem o opera — e por isso também representam a totalidade dos stakeholders do projeto: não há papel adicional (ex. investidor, fornecedor, órgão regulador) cujos interesses divirjam dos dessas duas personas dentro do escopo definido. Optou-se por não introduzir um "dono do negócio" como stakeholder separado, já que suas metas (Product Goals) já estão representadas pelos indicadores que o sistema entrega à atendente/gestora.

**Construção e priorização do backlog.** O backlog não foi priorizado arbitrariamente: passou por três filtros sucessivos. Primeiro, um workshop de Lean Inception gerou a lista bruta de funcionalidades (Feature Brainstorming) e uma primeira triagem por uma matriz de três eixos — esforço técnico, valor de negócio e valor de UX — que já eliminou o que tinha alto custo e baixo retorno (ex.: fila de espera, múltiplos canais, pagamento online), destinando-os ao backlog futuro. Segundo, um Sequencer organizou o que restou em ondas de dependência técnica (cadastros antes de agendamento, agendamento antes de notificações e indicadores). Terceiro, essa mesma ordem de dependência foi reclassificada em MoSCoW: os itens da base técnica (autenticação, cadastros, cálculo de duração, verificação de disponibilidade) e o fluxo de agendamento em si (agendar, bloquear overbooking) formam o Must have, porque nenhuma funcionalidade posterior tem sentido sem eles. Perfis de acesso e confirmação/lembrete formam o Should have — importantes para a meta de reduzir no-show, mas o sistema ainda opera (de forma mais arriscada) sem eles. Painel consolidado, indicadores e alertas de conflito formam o Could have — melhoram a gestão, mas não impedem o uso do produto. Reagendamento pelo cliente foi classificado como Won't have nesta versão, coerente com a decisão de escopo já tomada.

**Consistência geral.** Essa cadeia de decisões — problema → escopo reduzido → personas → features → priorização Effort×Business×UX → Sequencer → MoSCoW — mantém rastreabilidade: cada história do Must have pode ser justificada tanto pela dependência técnica quanto pelo valor de negócio, e nenhuma decisão de priorização contradiz os Product Goals definidos (reduzir no-show, aumentar ocupação, aumentar retenção).
