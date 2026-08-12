# System Design Document

## Visão Geral da Arquitetura

### 1. Modelos de Comunicação

- **Restful API**: Implementado com o framework Spring Boot utilizando as rotas definidas no arquivo `src/main/resources/config/routes.yml`. Estes rotas são gerenciados através dos endpoints do Swagger e podem ser acessadas por meio da URL.
- **SSE (Server-Sent Events)**: Para a comunicação de eventos, como mensagens enviamas em tempo real para clientes conectados à plataforma. Os dados são enviados via sockets em forma de stream continuo.
- **GRPC**: Aplicado ao serviço que faz a comunicação entre diferentes serviços da plataforma. Utilizando as bibliotecas do Google Protocol Buffers (protobuf), este protocolo é usado para transmissão rápida e segura de dados de alto volume.

### 2. Padrões de Implantação

- **Monolith First**: Para um início rápido, a arquitetura inicial se concentra em uma estrutura monolítica para testar o ambiente.
- **Microsserviços Políptos**: Após os primeiros teste passarem com sucesso, a plataforma é refeito e as funcionalidades são separadas em microsserviços. Utilizando um polígono de abordagem (Polyglot Architecture), diferentes linguagens podem ser utilizadas para implementar o mesmo serviço.

### 3. Mapeamento dos Bounded Contexts

- **Contexto do Domínio Pedidos**: Pertence à Linguagem Ubíqua (LUP) e está localizado na camada de transporte TCP. A comunicação é feita através da HTTP usando a rotas definidas no arquivo `src/main/resources/config/routes.yml`.
- **Contexto dos Serviços Faturamento**: Pertence à Linguagem Ubíqua (LUP) e está localizado na camada de transporte UDP. A comunicação ocorre entre serviços utilizando o protocolo gRPC.

## Contratos de Dados & Interfaces

### 1. OpenAPI (Swagger)

O arquivo `src/main/resources/config/routes.yml` foi utilizado para gerar o contrato REST usando o Swagger.

- **Endpoints do REST**:
    - `/pedidos`: Endpoint para consulta e manipulação dos pedidos.
    - `/faturamento`: Endpoint para gestão de faturamentos.
    - `/telemetria`: Endpoint para monitorar a qualidade da comunicação no sistema.

### 2. Schemas JSON / ProtoBuf

- **JSON**: Utilizado para as APIs REST e para o intercâmbio entre diferentes partes do projeto, como integrantes da plataforma, desenvolvedores de serviços micro e clientes.
- **Protobuf**: Utilizado para a comunicação entre os microsserviços implementados em linguagens diferentes.

A escolha por JSON permite um fluxo mais fluido e sem nenhuma necessidade de conversão manual, enquanto o Protobuf oferece uma transmissão rápida e segura de dados de alto volume. A camada TCP foi selecionada para as comunicações bidirecionais entre clientes e microserviços parceiros por sua capacidade de transmitir informações em tempo real e com baixo desempenho, que é o principal requisito do contexto Pedidos.

A camada UDP é escolhida para comunicações onde a latência não seja um problema crítico, como as interações entre os microserviços da plataforma. Uma vez atendido o requerimento de velocidade e qualidade de comunicação, será adotada uma abordagem que inclui a implementação em diferentes linguagens, como Node.js ou Python, para melhorar a flexibilidade do projeto.

### 3. Transportes Adicionais

- **TCP**: Utilizado na camada Pedidos para interações bidirecionais entre clientes e microserviços parceiros.
- **UDP**: Também utilizado na camada Faturamento para comunicações rápidas e altamente eficientes, como a monitoração dos serviços da plataforma.

A utilização do protocolo TCP se tornou necessária por causa de uma solicitação do cliente que exigiu interações mais precisas entre diferentes partes da plataforma. A implementação em UDP é adicional à camada Faturamento para melhorar o desempenho e a velocidade dos dados, seguindo os padrões definidos pelo requisito não funcional.

### 4. Justificativa

- **TCP**: Apesar do faturamento ser um serviço que recebe muitos pedidos simultâneos, a implementação em TCP é necessário por causa da necessidade de uma velocidade e qualidade de comunicação mais próxima às exigências do cliente. Além disso, este protocolo oferece transmissão semelhante ao UDP, mas com garantia de entrega.
- **UDP**: A escolha para a camada Faturamento é motivada pelo fato de que um serviço como o faturamento não precisa ter uma resposta tão imediata quanto a comunicação bidirecional entre clientes e parceiros. O protocolo UDP oferece velocidade rápida, mas também permite transmissões rápidas sem precisar se preocupar com o custo da latência, que é um elemento importante no contexto de faturamento.

## Conclusão

A abordagem SDD/Spec Driven Development apresenta uma visão clara e organizada do projeto, utilizando os principais princípios e métodos para o desenvolvimento contínuo. A documentação fornecida aqui é apenas um esboço inicial, mas representa as principais etapas necessárias para a criação de um sistema complexo como este.

O plano de implementação abrangente contempla todas as possíveis camadas de comunicação e microserviços da plataforma, permitindo que qualquer parte do projeto seja adotada ou modificada sem alterar o resto. Esta abordagem simplifica significativamente a criação de uma arquitetura robusta, garantindo assim um processo mais ágil e eficiente para desenvolvimento e implementação.

### Documentação Visual

A documentação visual pode ser elaborada através da geração do diagrama do sistema (System Diagram) utilizando ferramentas como PlantUML ou similar. Este diagrama seria uma forma visual clara das camadas de comunicação, microserviços, rotas RESTful e APIs gRPC utilizadas na plataforma.

A documentação será revisada, aprovada e atualizada regularmente para manter o projeto em sintonia com as necessidades do cliente. O plano SDD/Spec Driven Development permite uma gestão eficaz da complexidade deste sistema, oferecendo orientações claras sobre o processo de implementação contínuo.
