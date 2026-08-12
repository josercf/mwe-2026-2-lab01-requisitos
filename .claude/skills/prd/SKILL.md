---
name: prd-authoring
description: Metodologia e padrão para criação de Product Requirement Documents (PRD) estruturados para sistemas web enterprise e soluções com Inteligência Artificial.
---

# PRD Authoring Skill — Padrão de Requisitos de Produto

Esta skill orienta o planejamento e escrita de um **PRD (Product Requirement Document)** completo para guiá-lo no ciclo de vida de desenvolvimento de software (SDLC).

## Estrutura do PRD

### 1. Visão do Produto & Problema de Negócio
- **Problema:** Qual dor do usuário ou gargalo operacional está sendo resolvido?
- **Visão:** Qual a proposta de valor da solução?
- **Público-Alvo:** Personas (ex.: Operador Logístico, Cliente B2B, Motorista).

### 2. Casos de Uso (Use Cases)
- **UC01 - [Nome do Caso de Uso]:**
  - **Ator:** Quem executa.
  - **Pré-condição:** Estado inicial do sistema.
  - **Fluxo Principal:** Passo a passo do comportamento.
  - **Critérios de Aceite:** Regras objetivas para considerar a funcionalidade concluída.

### 3. Requisitos Não-Funcionais (RNFs) & SLAs
- Desempenho (RPS, tempo de resposta p95/p99).
- Segurança (OAuth2, OIDC, RBAC).
- Escalabilidade e Conteinerização (Docker/Kubernetes).

---
*Referências: PM3, Atlassian Product Management, GitHub Awesome Copilot Skills.*
