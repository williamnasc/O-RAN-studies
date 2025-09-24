# Near-RT RIC Funcional Description

## Descrição Geral

![Arquitetura Geral do Near-RT RIC](figs/near_rt_architecture.png)

Um Near-RT RIC é composto por uma plataforma Near-RT RIC e um ou mais xApps. Uma visão geral é mostrada na Figura acima. A Figura também mostra as funcionalidades da plataforma Near-RT RIC. Essas funcionalidades serão descritas mais detalhadamente a seguir.

## Funcionalidades da Plataforma Near-RT RIC

### Base de dados e SDL (Shared Data Layer)

As funcionalidades do banco de dados e SDL permitem que a plataforma Near-RT RIC armazene e disponibilize informações de RAN/UE e outras informações necessárias para apoiar casos de uso específicos.

- **UE-NIB**: Funcionalidade que mantém informações relacionadas ao UE. Exemplos são:
  - Manutenção de uma lista de UEs e dados associados; 
  - Rastreamento e correlação das identidades dos UEs associadas aos Nós E2 conectados. 
  
- **R-NIB**: Funcionalidade que mantem informações relacionadas à RAN
  - Informações dos nós E2 e o mapeamento entre eles;

Essas informações podem ser geradas pelo RIC ou xApps;

- **SDL**: Funcionalidade que disponibiliza os serviços de SDL para os xApps.
  - Permite acesso e manipulação no banco de dados, R-NIB e UE-NIB e outro casos de usos específicos.

### xApp Subscription Management

Essa funcionalidade permite gerenciamento solicitações de assinatura de diferentes xApps para dados relacionados ao E2 e forneça uma distribuição de dados unificada para xApps desses dados:

- Gerencimento de assinaturas de xApps para nós E2;
- Aplição políticas de controle de acesso de xApps às mensagens; 
- Agregação de assinaturas idênticas de diferentes xApps em uma única assinatura para um nó E2; 
- Auditoria das assinaturas existentes; 
- Correção de problemas associadas.

### Conflict Mitigation

Funcionalidade para detecção e resolução de solicitações sobrepostas ou conflitantes de múltiplos xApps.

Isso ocorre por que um xApp normalmente mudará um ou mais parâmetros com o objetivo de otimizar uma métrica específica. 

### Messagin Infrastructure

Essa funcionalidade para entrega de mensagens de baixa latência entre os pontos finais internos do Near-RT RIC.

- Suporta registro/descoberta/exclusão de endpoints
- Forcene uma API para enviar e outra para receber mensagens;
- Suporta tipos diferentes de mensagens, exemplos:
  - ponto-ponto;
  - ponto-multiponto;
- Sistema de roteamento das mensagens;
- Robustez para evitar perda de dados;

### Security

- Funcionalidade de segurança interna. 

- Os requisitos de segurança para o eNB LTE e para o gNB NR de 5G estão definidos pelo 3GPP.

- Um dos objetivos é prevenir que xApps maliciosos. Exemplos são:
  - Exportar dados para sistemas externos não autorizados;
  - Abuso das capacidades de controle sobre as funções RAN; 

### Management

- Responável por OAM management no Near-RT RIC;
- **OAM management**: Gereciamento de falha, configuração, desempenho, arquivo, segurança e outros serviços de gerenciamento.
  - Gerencimento de falta;
  - Gerenciamento de Configuração;
  - Sistema de Logs;
  - Tracing (monitoramento de transações ou fluxos);
  - Coleta de Metricas;

### Interface Termination

Funcionalidade que conecta as intercaces com o RIC.

Cada interface apresenta seus respectivos serviços e capacidades.

#### E2 Termination

- Conexão SCTP (Stream Control Transmission Protocol) de cada Nó E2;
- Roteamento de mensagens dos xApps para os Nós E2.
- Manipulação das mensagens de relacionadas a E2 connectivity;
- Recebimento e resposta dos E2 Setup Request;
- Notificar xApps da lista de funções de rede suportadas pelo nó E2;
- Notificar a um Nó E2 da lista de funções aceitas;

**obs:** O SCTP é um protocolo de transporte da camada de rede usado para transportar mensagens de sinalização de telecomunicações.

### A1 Termination

Permite o uso da interface A1.
- Fornece API genérica para enviar e receber mensagens via A1
  - Politicas A1;
  - Informações do Non-RT RIC;
  - Feedbacks de politicas A1 para o Non-RT RIC;
- Envio de Politicas A1 para os xApps;

#### O1 Termination

Permite o uso da interface O1.

A Plataforma produz serviços de gerenciamento (management services), chamados de MnS que são consumidos pelo SMO via O1;

- Serviços de gerenciamento de provisionamento do RIC via O1; 
- Traduzir serviços de gerenciamento O1 para as APIs do RIC; 
- Serviços de FM (Fault Management) para relatar falhas e eventos do RIC via O1; 
- Serviços de PM para relatar dados de PM via O1; 
- Serviços de gerenciamento de arquivos 
  - Baixar 
    - arquivos de ML, arquivos de software, etc. e 
  - Upload 
    - arquivos de log/trace; 
- Serviços de vigilância de comunicação na O1.

#### Y1 Termination

Permite o uso da interface Y1. 
- Suporte para expor informações analíticas de RAN pela Y1.

### API Enablement
 
 As APIs do Near-RT RIC podem ser 
 - Categorizaras com base na interação com a plataforma 
 - Estar relacionadas a serviços relacionados a
   - E2, 
   - A1, 
   - Gerenciamento (Management), 
   - SDL.

Essa funcionalidade oferece suporte para o funcionamento das APIs Near-RT RIC

Os serviços da API Enablement incluem:
- Registro/Armazenamento das APIs;
- Descoberta as APIs registradas;
- Autenticação do xApps para usar as APIs;
- Evitar conflitos de compatibilidade entre xApps e os serviços q eles acessem;

As APIs são habilitadas de acordo com os níveis de confiança dos xApps.

### AI/ML Support

A funcionalidade capacita com 
- Suporte completo ao fluxo de trabalho de IA/ML para os xApps. 
- Os xApps podem usar nenhum, parte ou toda essa funcionalidade, dependendo de seu design.

As funcionalidades disponíveis pelo AI/ML Support são:
- Data Pipelining
- Model Management
- Training
- Inference

### xApp Repositpry Function

Essa Funcionalidade que permite:
 
- Manter uma lista de candidatos xApp(s) para Terminação A1 para enviar política A1 ou atualização de política para xApp(s) adequados com base no tipo de política e nas políticas do operador;

- Manter os tipos de políticas suportadas. 
  - Baseados nas políticas suportados pelos xApps e políticas do operador; 

- Realizar controle de acesso a xApp para o tipo A1-EI solicitado com base nas políticas do operador.

## Funcionalidades dos xApps

- Atender casos de uso especializados.

- Colaborar com a plataforma para Mitigação de Conflitos relacionados ao E2.

- Melhorar a capacidade de RRM (Radio Resource Management) na RAN.

- Utiliza zero, um ou mais E2SMs (E2 Service Models).

- Ao ser registrar, informa ao RIC suas informações de OAM e controle para habilitar funcionalidades relevantes.

