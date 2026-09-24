# Entrega 1 — Backlog Inicial

**Disciplina:** Macro-Módulo V — Projeto Integrador — Laboratório Ágil (LAER)
**Data de conclusão:** 28/09/2026

## Integrantes do Grupo

Vinicius Andrade · Thiago Alheiros · Vinicius Brito · Álvaro · João Pedro · Vicktoria

## Produto e Problema

**PetSlot** — sistema de agendamento para banho e tosa de pets. Agendamento informal (telefone, agenda física, mensagens) não considera a duração variável do atendimento por porte/pelagem do animal, nem a disponibilidade real de tosadores e boxes — gerando overbooking, atrasos em cadeia e faltas sem aviso (no-show), com impacto direto na receita e na experiência do cliente.

## Personas e Stakeholders

**Marcos (cliente):** tutor de pet que agenda banho/tosa pelo celular; quer horário rápido, sem risco de conflito.

**Atendente/gestora:** gerencia a agenda de tosadores e boxes; precisa de visão unificada e alertas de conflito.

As duas personas cobrem a totalidade dos stakeholders do projeto — não há papel externo adicional, já que os objetivos de negócio são atendidos diretamente pelos indicadores entregues à gestora.

## Product Backlog e Priorização (MoSCoW)

Critérios de aceitação completos, em formato BDD (Given/When/Then), estão documentados como sub-issues no repositório: **github.com/Viniswitch/PetSlot**.

| # | História | Critério de aceite (resumo) | Prioridade |
|---|---|---|---|
| US01 | Login/Autenticação | Acesso liberado com credenciais válidas; erro caso contrário | Must |
| US02 | Cadastro de Cliente | Conta criada com nome+contato; contato duplicado é rejeitado | Must |
| US03 | Cadastro de Pets | Pet cadastrado com porte/pelagem; dados incompletos bloqueiam o cadastro | Must |
| US04 | Cadastro de Tosadores | Tosador cadastrado com horário de trabalho; agendamento fora do horário é impedido | Must |
| US10 | Cadastro de Boxes | Box cadastrado como recurso; box já ocupado bloqueia novo agendamento simultâneo | Must |
| US11 | Cálculo Automático de Duração | Duração do atendimento calculada automaticamente por porte/pelagem | Must |
| US06 | Verificação de Disponibilidade em Tempo Real | Só horários com tosador e box livres são exibidos, atualizando em tempo real | Must |
| US12 | Agendamento Online | Agendamento vincula cliente/pet/tosador/box; horário indisponível é recusado | Must |
| US13 | Bloqueio Anti-Overbooking | Agendamento é rejeitado se tosador ou box já estiverem reservados no horário | Must |
| US05 | Perfis de Acesso | Cliente não acessa telas administrativas; equipe acessa as suas | Should |
| US07 | Confirmação e Lembrete Automático | Confirmação enviada ao concluir agendamento; lembrete enviado antes do horário | Should |
| US08 | Painel Geral da Agenda | Painel exibe agenda consolidada de todos os tosadores/boxes por dia/semana | Could |
| US09 | Indicadores de Ocupação e No-show | Painel exibe taxa de ocupação e no-show, recalculadas por período | Could |
| US14 | Alertas de Conflito | Alerta exibido no painel ao detectar sobreposição de recursos | Could |
| US15 | Reagendamento e Cancelamento | Cancelamento libera o horário; reagendamento segue as mesmas regras de disponibilidade | Won't (this time) |

*Conferência: Must ≈ 62% do esforço total (em pontos) — dentro do razoável (~60%), a priorização não ficou "achatada".*

## Justificativa Técnica das Decisões

O escopo original (agendamento integrado a três serviços — banho/tosa, veterinário e hospedagem) foi reduzido para cobrir apenas banho e tosa, evitando a complexidade de modelar conflitos entre categorias de recursos distintas sem alterar a natureza do problema central (overbooking e no-show por falta de controle de disponibilidade).

As duas personas definidas cobrem os dois lados de qualquer transação do sistema — quem consome o serviço e quem o opera — e por isso também representam a totalidade dos stakeholders; não há papel adicional cujos interesses divirjam dos dessas personas dentro do escopo definido.

O backlog passou por três filtros sucessivos antes da priorização final: (1) um Lean Inception gerou a lista bruta de funcionalidades e uma triagem por esforço técnico × valor de negócio × valor de UX, já descartando itens de alto custo e baixo retorno para o backlog futuro; (2) um Sequencer organizou o que restou em ondas de dependência técnica; (3) essa mesma ordem foi reclassificada em MoSCoW — a base técnica e o fluxo de agendamento formam o Must have (nada posterior funciona sem eles), perfis de acesso e notificações formam o Should have, painel e indicadores formam o Could have, e reagendamento ficou como Won't have nesta versão, coerente com a redução de escopo já decidida.

Essa cadeia — problema → escopo → personas → features → matriz Effort×Business×UX → Sequencer → MoSCoW — mantém rastreabilidade: cada história do Must have é justificável tanto por dependência técnica quanto por valor de negócio, e nenhuma prioridade contradiz os objetivos definidos (reduzir no-show, aumentar ocupação, aumentar retenção).
