# Entrega 4 — RNF e Arquitetura

**Disciplina:** Macro-Módulo V — Projeto Integrador — Laboratório Ágil (LAER) · **Entrega:** 19/10/2026
**Produto:** PetSlot · **Repositório:** github.com/Viniswitch/PetSlot

**Integrantes:** Vinicius Andrade · Thiago Alheiros · Vinicius Brito · Álvaro · João Pedro · Vicktoria

## Requisitos Não Funcionais

| ID | Categoria | Requisito (meta) | Histórias |
|---|---|---|---|
| RNF01 | Desempenho | A lista de horários disponíveis carrega em até 3 s | US06, US11, US12 |
| RNF02 | Desempenho | Painel da agenda e indicadores carregam em até 5 s | US08, US09 |
| RNF03 | Segurança | Telas administrativas só abrem para o perfil equipe, por qualquer caminho (menu ou URL) | US05, US08, US09, US14 |
| RNF04 | Segurança | Senhas nunca ficam em texto puro; a transmissão é criptografada | US01, US02 |
| RNF05 | Usabilidade | O cliente agenda pelo celular em até 5 passos | US03, US06, US12 |
| RNF06 | Confiabilidade | Tosador ou box nunca tem duas reservas no mesmo horário, mesmo com acessos simultâneos | US10, US12, US13 |
| RNF07 | Integridade de dados | Entradas são validadas e normalizadas: telefone sem formatação; campo só com espaços conta como vazio | US02, US03 |

Metas numéricas são metas de projeto, definidas pelo grupo.

## Decisões Arquiteturais

| ID | Decisão | RNFs | Justificativa técnica |
|---|---|---|---|
| AD01 | Arquitetura cliente-servidor em camadas: interface web → regras de negócio → banco de dados | RNF03, RNF06 | As regras ficam no servidor; a interface não decide nada que afete segurança ou conflito |
| AD02 | Interface web responsiva, desenhada primeiro para celular | RNF05 | A persona Marcos agenda pelo celular; evita app nativo e reduz custo |
| AD03 | Autorização por perfil validada no servidor, em cada rota | RNF03 | Esconder o menu não bloqueia a URL direta (BUG03) |
| AD04 | Senhas com hash e salt; tráfego por HTTPS | RNF04 | Vazamento da base não expõe senhas; dados protegidos em trânsito |
| AD05 | Banco relacional com restrição de unicidade (tosador/box + horário) e reserva em transação | RNF06 | O banco rejeita a reserva dupla mesmo com dois clientes ao mesmo tempo; a regra não depende só da aplicação |
| AD06 | Camada única de validação e normalização de entrada, usada por todos os cadastros | RNF07 | Corrige na origem as causas de BUG01 e BUG02, em vez de tratar tela a tela |
| AD07 | Índices por data, tosador e box; consultas limitadas ao período exibido | RNF01, RNF02 | Mantém a resposta rápida conforme os agendamentos crescem |

## Rastreabilidade

Origem → RNF → decisão → histórias:

- **BUG03 (#46)** → RNF03 → AD03 (e AD01) → US05, US08, US09, US14
- **BUG01 (#44) e BUG02 (#45)** → RNF07 → AD06 → US02, US03
- **Problema central (overbooking)** → RNF06 → AD05 (e AD01) → US10, US12, US13
- **Persona Marcos (celular)** → RNF05 → AD02 → US03, US06, US12
- **Necessidade de horário rápido (Marcos)** → RNF01 → AD07 → US06, US11, US12
- **Necessidade de visão única (gestora)** → RNF02 → AD07 → US08, US09
- **Proteção de credenciais** → RNF04 → AD04 → US01, US02

Todo RNF tem ao menos uma decisão, e toda decisão responde a ao menos um RNF.
