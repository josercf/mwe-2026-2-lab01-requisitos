---
name: sdd-spec-driven
description: Metodologia de Specification Driven Development (SDD) e Arquitetura de Software baseada em Domain-Driven Design (DDD).
---

# SDD Spec Driven Development Skill

Esta skill define o padrão de documentação de design de sistema (**System Design Document**) e especificações formais de software antes da codificação.

## Estrutura do SDD

### 1. Visão Geral da Arquitetura
- Modelo de comunicação (REST, SSE, Sockets, gRPC).
- Padrão de implantação (Monolith-First vs Microsserviços Poliglotas).

### 2. Mapeamento de Bounded Contexts (DDD)
- Definição dos limites de domínio (ex.: Pedidos, Faturamento, Telemetria).
- Matriz de Linguagem Ubíqua para alinhamento entre negócio e engenharia.

### 3. Contratos de Dados & Interfaces
- Especificação OpenAPI (Swagger) para APIs REST.
- Schemas JSON / ProtoBuf para comunicação entre serviços.

## 4. System Design Document

### 4.1 Visão Geral
O documento de design especifica os contextos de domínio, os termos de negócio e as decisões de transporte que suportam os requisitos funcionais e não-funcionais.

### 4.2 Bounded Contexts Identificados
- **Pedido**: gerencia a criação, validação e estado de pedidos de compra.
- **Faturamento**: processa cobranças, notas fiscais e confirmação de pagamento.
- **Telemetria**: coleta métricas e eventos de operação para monitoramento e alertas.
- **Catálogo**: mantém informações de produtos, preços e disponibilidade.
- **Notificação**: envia alertas e confirmações aos usuários.

### 4.3 Linguagem Ubíqua
- **Pedido**: solicitação de compra enviada pelo cliente.
- **Item do Pedido**: produto ou serviço associado a um pedido.
- **Pagamento**: transação financeira para liquidar um pedido.
- **Fatura**: documento que formaliza o valor a ser cobrado.
- **Evento de Telemetria**: sinal emitido para monitorar estado e desempenho.
- **Disponibilidade**: capacidade do sistema de responder a consultas de catálogo.
- **Latência**: tempo máximo aceitável entre envio e recebimento de dados.
- **Confiabilidade**: garantia de entrega sem perda de mensagens críticas.

### 4.4 Camada de Transporte para Cada Fluxo de Dados
- **Fluxo Cliente -> Pedido**: REST/HTTP sobre TCP.
  - Justificativa: os requisitos não-funcionais de consistência e integridade de pedidos exigem entrega confiável e ordenada. TCP atende a estes requisitos melhor que UDP.
- **Fluxo Pedido -> Faturamento**: API interna via REST ou gRPC sobre TCP.
  - Justificativa: dados de cobrança e faturamento demandam transações seguras e auditáveis. A entrega confiável de cada mensagem é essencial, portanto TCP é a camada adequada.
- **Fluxo Pedido -> Telemetria**: envio de eventos de observabilidade por protocolo leve, preferencialmente UDP para métricas de alta frequência.
  - Justificativa: a telemetria tem um requisito não-funcional de baixa latência e alta taxa de transferência; ela pode tolerar perda ocasional de pacotes não críticos. UDP reduz overhead e melhora desempenho.
- **Fluxo Catálogo -> Cliente/Front-end**: REST/HTTP sobre TCP.
  - Justificativa: consultas de produto exigem dados consistentes e completos para evitar exibir informação incorreta ao usuário. TCP garante confiabilidade no transporte.
- **Fluxo Notificação -> Usuário**: entrega de alertas via canais confiáveis sobre TCP.
  - Justificativa: notificações de status e confirmação de transação são críticas para experiência do usuário. Requer-se entrega confiável e rastreável, tornando TCP a escolha apropriada.

### 4.5 Resumo das Decisões de Transporte
- Use **TCP** quando o requisito não-funcional prioriza confiabilidade, integridade de dados e consistência transacional.
- Use **UDP** quando o requisito não-funcional prioriza baixa latência e alta taxa de envio, com tolerância a perda de pacotes em fluxos de telemetria ou métricas.

---
*Referências: GitHub Spec Kit, Pressman & Sommerville Software Engineering.*
