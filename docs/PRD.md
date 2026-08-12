```markdown
```

# PRD — Serviço de Telemetria de Frota — LogiTech

## Visão do Produto

Prover um serviço de telemetria que permita à LogiTech rastrear em tempo adequado a localização, status e condições das cargas transportadas por sua frota de 400 caminhões, reduzindo incertezas entre coleta e entrega, melhorando visibilidade operacional, segurança e satisfação do cliente.

## Problema

Atualmente a LogiTech não tem visibilidade confiável da localização e do estado da carga entre a coleta e a entrega. Isso resulta em: atrasos não detectados, dificuldade na comunicação com clientes, risco aumentado de perda ou avaria da carga e ineficiências operacionais que elevam custos.

## Personas

- Gerente de Operações (Mariana): responsável pelo despacho e monitoramento da frota; precisa reagir rapidamente a desvios e comunicar clientes.
- Coordenador de Rastreio (Pedro): monitora entregas em andamento e investiga incidentes; precisa de dados confiáveis sobre posição e status da carga.
- Motorista (Carlos): realiza coletas e entregas; precisa de instruções claras e meios simples de reportar problemas.
- Cliente (Empresa Alpha): espera confirmação de coleta, previsão de entrega e notificação em caso de atraso ou problema.

## Casos de Uso

1. Visualizar posição atual de um caminhão e da carga associada.
2. Receber alerta quando um veículo desvia da rota planejada ou fica parado por tempo excessivo.
3. Registrar status da carga na coleta e na entrega (ex.: condição, lacre, temperatura) e poder consultar histórico.
4. Consultar cronograma estimado de chegada (ETA) por entrega e atualizar clientes quando houver atraso relevante.
5. Motorista reporta manualmente incidente (avaria, acidente, roubo) e registra evidências.
6. Gerar relatórios periódicos de performance da frota (tempo de viagem, paradas, incidentes).

## Requisitos Funcionais (verificáveis, com identificador)

- RF-01: O sistema deve permitir consultar a localização atual de qualquer caminhão da frota em um mapa com carimbo de data/hora. (verificação: consulta retorna coordenadas e timestamp).
- RF-02: O sistema deve registrar e disponibilizar o histórico de posições de um veículo por pelo menos 90 dias. (verificação: histórico exportável com registros por data).
- RF-03: O sistema deve criar alertas quando um veículo permanecer parado por mais de um limite configurável (por padrão 30 minutos). (verificação: alertas registrados quando condição ocorre).
- RF-04: O sistema deve permitir registrar o status da carga na coleta e na entrega (incluindo campos: condição, lacre, fotos) e associá-lo a um evento de entrega. (verificação: registro de evento com campos preenchidos).
- RF-05: O sistema deve enviar notificações (visíveis a usuário do sistema) quando um evento crítico ocorrer: desvio de rota, atraso acima de limite configurável ou incidente reportado. (verificação: notificação criada e entregue conforme evento).
- RF-06: O sistema deve permitir que motoristas registrem incidentes com texto e anexos (ex.: fotos) vinculados a um veículo e a uma viagem. (verificação: incidente criado com anexos associados).
- RF-07: O sistema deve gerar relatórios de desempenho da frota (tempo médio de viagem, número de incidentes, tempo de parada) para intervalos de datas selecionados. (verificação: relatório gerado contendo métricas solicitadas).
- RF-08: O sistema deve expor pesquisa por número de entrega, placa do veículo ou intervalo de datas e retornar registros relacionados. (verificação: busca retorna resultados corretos para critérios dados).

## Requisitos Não Funcionais (verificáveis, com identificador)

- RNF-01: Disponibilidade: o serviço deve estar disponível 99% do tempo em uma janela mensal. (verificação: monitoramento de uptime mensal).
- RNF-02: Latência: consultas de localização devem responder em menos de 2 segundos para 95% das requisições. (verificação: métricas de latência coletadas e analisadas).
- RNF-03: Escalabilidade: o sistema deve suportar simultaneamente atualização de posições de até 400 veículos com picos de até 2 atualizações por segundo por veículo. (verificação: testes de carga simulando 800 atualizações/s).
- RNF-04: Persistência: dados de telemetria e registros devem ser mantidos por pelo menos 90 dias e backups periódicos devem ser comprováveis. (verificação: checagem de retenção e backups).
- RNF-05: Segurança e confidencialidade: acessos ao sistema devem ser autenticados e logs de auditoria devem registrar quem acessou ou modificou registros críticos. (verificação: existência de logs de auditoria e rastreabilidade de acessos).
- RNF-06: Integridade dos dados: as posições registradas devem incluir timestamp e fonte (manual/automática) e não podem ser aceitas entradas sem esses campos. (verificação: validação de entradas em amostra).
- RNF-07: Usabilidade: usuários chave (Gerente de Operações, Coordenador de Rastreio, Motorista) devem completar tarefas críticas (consultar localização, registrar incidente, registrar entrega) com sucesso em testes com taxa de sucesso >= 90%. (verificação: testes de usabilidade documentados).

## Métricas de Sucesso

- Redução de consultas manuais por clientes sobre status de entrega em 70% nos primeiros 6 meses.
- Redução do tempo médio de resposta a incidentes em 50% nos primeiros 6 meses.
- Cobertura de rastreamento: >= 95% das viagens registrando posição em intervalos esperados (conforme RNF de atualização) após implantação.
- Precisão de informação: discrepâncias entre localização reportada e verificada por auditoria abaixo de 2% em amostras trimestrais.
- Adoção: 100% dos motoristas usando o mecanismo de registro de incidentes e entregas em campo dentro de 3 meses.

---

Observação: Este documento descreve necessidades e critérios verificáveis. Não propõe soluções técnicas ou arquiteturais.
```
