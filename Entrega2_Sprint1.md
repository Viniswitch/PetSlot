# Entrega 2 — Sprint 1

**Disciplina:** Macro-Módulo V — Projeto Integrador — Laboratório Ágil (LAER) · **Entrega:** 01/10/2026
**Produto:** PetSlot · **Repositório:** github.com/Viniswitch/PetSlot

**Integrantes:** Vinicius Andrade · Thiago Alheiros · Vinicius Brito · Álvaro · João Pedro · Vicktoria

## Sprint Planning

- **Objetivo:** base de autenticação e cadastro
- **Período:** 17/09 a 01/10/2026
- **Histórias selecionadas:** US01 a US05 (Epic E01, #1)
- **Compromisso:** 14 pontos (Planning Poker)

## Sprint Backlog

Situação em 28/09/2026:

| História | Pontos | Status | Observação |
|---|---|---|---|
| US01 Login/Autenticação (#24) | 2 | Done | — |
| US04 Cadastro de Tosadores (#23) | 3 | Done | — |
| US02 Cadastro de Cliente (#25) | 2 | Doing | Bloqueada por BUG01 (P1) |
| US03 Cadastro de Pets (#26) | 2 | Doing | Bloqueada por BUG02 (P2) |
| US05 Perfis de Acesso (#27) | 5 | Doing | Bloqueada por BUG03 (P0) |

## Definição de Pronto (DoD)

Vale para todo o projeto (`DEFINITION_OF_DONE.md`). Uma história vai para Done quando:

- Critérios de aceite (BDD) testados
- Sem bug P0 ou P1 aberto vinculado
- Bug P2 só como dívida técnica, com decisão registrada (o grupo não aceitou o BUG02)
- Revisada por outro integrante

## Registro da Execução

Testes e bugs simulados, conforme orientação da professora.

- **18/09:** US01 a US05 criadas e vinculadas ao Epic E01
- **24/09:** 10 casos de teste executados (7 passaram, 3 falharam); bugs registrados no Epic E06 (#43); US01 e US04 em Done
- **28/09:** por orientação da professora, os bugs não são corrigidos na sprint

| Bug | História | Severidade | Teste | Descrição |
|---|---|---|---|---|
| BUG01 (#44) | US02 | P1 | TC04 | Duplicidade não detectada com telefone em formato diferente |
| BUG02 (#45) | US03 | P2 | TC06 | Campo só com espaços aceito como preenchido |
| BUG03 (#46) | US05 | P0 | TC10 | Tela administrativa acessível por URL direta |

## Velocity

**5 pontos** (US01 = 2 + US04 = 3) de 14 comprometidos (36%). Os 9 pontos restantes estão bloqueados por bugs.

## Burndown

Pontos restantes por período; a linha ideal desce 1 ponto por dia.

| Período | Ideal | Real |
|---|---|---|
| 17/09 a 23/09 | 14 → 8 | 14 |
| 24/09 | 7 | 9 |
| 25/09 a 28/09 | 6 → 3 | 9 |
| 29/09 a 01/10 (previsto) | 2 → 0 | 9 |

O real cai de 14 para 9 em 24/09 (US01 e US04 em Done) e permanece assim, pois os bugs não serão corrigidos na sprint.

*Sprint Review e Retrospectiva: realizadas em aula.*
