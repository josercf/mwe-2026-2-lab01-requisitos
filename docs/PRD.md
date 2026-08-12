### Visão do Produto & Problema de Negócio

**Problema:** O problema principal do usuário é encontrar o caminhão corretamente na frota, especialmente para cargas em transito.

**Visão:** Propor uma solução que permita aos operadores logísticos visualizar e gerenciar facilmente as informações dos seus caminhões, incluindo a localização atual, estado de carga (como "carregando", "desligado" ou "em transporte"), além das metas diárias de entrega.

**Público-Alvo:** Personas:
- **Operador Logístico:** Existe um número grande de operadores logísticos que precisam encontrar rapidamente o caminhão correto para realizar suas tarefas diariamente.
- **Motorista de Transporte:** Motoristas precisarão localizar seu veículo na frota, incluindo a carga em transito.

### Casos de Uso (Use Cases)

#### UC01 - Visualização do Caminhão
- **Ator:** Operador Logístico e Motorista.
- **Pré-condição:** O caminhão e o motorista estão listados na frota da empresa.
- **Fluxo Principal:** 
  - Visualize as informações do veículo (chave, placas, modelo, etc.)
  - Verifique a carga em transito (se houver) e sua localização atual.

#### UC02 - Atualização de Status
- **Ator:** Operador Logístico.
- **Pré-condição:** A carga está no caminhão ou na frota.
- **Fluxo Principal:**
  - Informe o status da carga (como "carregando", "desligado" ou "em transporte").
  - Adicionar, remover ou alterar metas de entrega.

#### UC03 - Visualização de Metas Diárias
- **Ator:** Operador Logístico.
- **Pré-condição:** Há metas diárias definidas para a operação da frota.
- **Fluxo Principal:**
  - Verifique as metas diárias atuais e as previstas (se houver).
  - Adicionar, alterar ou remover metas.

#### UC04 - Informações do Caminhão
- **Ator:** Operador Logístico e Motorista.
- **Pré-condição:** O caminhão está listado na frota da empresa.
- **Fluxo Principal:**
  - Visualize informações úteis como número de caminhões, ano de manutenção, status técnico (como "próximo escaneamento").

### Requisitos Não-Funcionais (RNFs) & SLAs

#### Desempenho
- **RPS:** Tempo médio para visualizar o status da carga em 95% das tentativas.
- **Tempo de Resposta p95/p99:** Até 1 segundo, garantindo uma resposta rápida.

#### Segurança
- **OAuth2:** Autorização dos usuários logados nas configurações do sistema.
- **RBAC (Requisitos Baseados em Função):** Restrições funcionais para evitar que o usuário altere dados de outras operações.
- **HTTPS/SSL Certificado:** Autenticação segura com SSL.

#### Escalabilidade e Conteinerização
- **Docker/Kubernetes:** Instalação automática dos componentes necessários do sistema, permitindo manusear facilmente a escala da frota de caminhões.

Por fim, a proposta é que o operador logístico ou motorista possa visualizar e gerenciar as informações dos seus caminhões através de um aplicativo web simples e intuitivo, resolvendo assim uma das principais dificuldades enfrentadas pelas empresas de transporte.
