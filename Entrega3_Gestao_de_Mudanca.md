# Entrega 3 — Gestão de Mudança

**Disciplina:** Macro-Módulo V — Projeto Integrador — Laboratório Ágil (LAER) · **Entrega:** 01/10/2026
**Produto:** PetSlot · **Repositório:** github.com/Viniswitch/PetSlot

**Integrantes:** Vinicius Andrade · Thiago Alheiros · Vinicius Brito · Álvaro · João Pedro · Vicktoria

## Mudança de Requisito

Origem: os bugs encontrados nos testes da Sprint 1. Cada um expôs um caso de borda que o critério de aceite original não explicitava.

| ID | História | Requisito original | Mudança solicitada | Motivo |
|---|---|---|---|---|
| MR01 | US02 (#25) | Cadastro duplicado é impedido (mesmo telefone/e-mail) | Comparar telefone ignorando a formatação | BUG01: número com formatação diferente aceito como novo |
| MR02 | US03 (#26) | Porte e pelagem são obrigatórios | Campo só com espaços conta como não informado | BUG02: pelagem só com espaço aceita |
| MR03 | US05 (#27) | Cliente é bloqueado ao acessar tela administrativa | Bloqueio vale para menu e URL direta (permissão validada por rota) | BUG03: tela administrativa aberta por URL |

## Análise de Impacto

- **MR01:** afeta US02 e US12 (o agendamento exige cliente); risco médio (P1)
- **MR02:** afeta US03 e US11 (a duração usa porte e pelagem); risco baixo (P2)
- **MR03:** afeta US05 e as telas administrativas de US08, US09 e US14; risco alto (P0, segurança)
- **Planejamento:** a Sprint 1 fecha com 5 de 14 pontos; replanejar US02, US03 e US05 (9 pontos) na Sprint 2 elevaria a carga de 12 para 21 pontos, contra velocity de 5
- **Prioridade:** a US05 (Should) merece reavaliação para Must, por ser falha P0

## Decisão Tomada

1. Refinar o critério BDD de US02, US03 e US05, com um cenário novo cada
2. Não corrigir os bugs nesta sprint (orientação da professora); as histórias seguem bloqueadas, conforme a DoD
3. BUG02 (P2) não aceito como dívida técnica (decisão do grupo)

**Justificativa**

- Causa comum: os critérios cobriam só o caminho principal; corrigir o critério na origem evita reincidência
- Corrigir só o código deixaria o requisito ambíguo e sem cenário de regressão
- Manter a sprint fechada preserva o planejamento; a correção entra como trabalho planejado no Epic E06

## Alterações no Backlog

- Epic E06 — Correção de Defeitos criado (#43); BUG01 a BUG03 (#44 a #46) registrados nele
- US02, US03 e US05: vínculo "blocked by" com o bug correspondente; status mantido em Doing
- US02, US03 e US05: novo cenário BDD no critério de aceite, referenciando MR01, MR02 e MR03

## Rastreabilidade

- **MR01:** TC04 → BUG01 (#44) → US02 (#25) → E01 (#1)
- **MR02:** TC06 → BUG02 (#45) → US03 (#26) → E01 (#1)
- **MR03:** TC10 → BUG03 (#46) → US05 (#27) → E01 (#1)

Bugs agrupados no E06 (#43). No GitHub: campo "Relationships" (blocked by) e histórico de edição das issues.
