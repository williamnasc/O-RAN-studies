# Arquitetura O-RAN

A arquitetura pode ser apresentada em diferentes escopos

### Arquitetura em Alto Nível

![High Level Arq](figs/high_level.png)

Nessa perspectiva, temos 4 grandes entidades,
- O sistema de geranciamento e orquestração,
onde se encontra o Non-RT RIC;
- As funções de rede da RAN,
onde se encontra o Near-RT RIC;
- A parte de processamento em núvem;
- e o Núcleo da rede;

Entre essas entidades temos as interfaces:

- A1
- O1
- Open Fronthaul M-plane
- e A2

Conectando o Frameworkd de SMO (Service Management and Orchestration)
com as funções de rede (O-RAN Network Functions)
e os recursos em núvem (O-Cloud).

Como mostrado na Figura, o O-Cloud tem uma interface de notificação
para as funções de rede O-RAN

Isso também ilustra que as funções de rede O-RAN podem ser hospedadas
em um hardware customizado ou na O-Cloud;

Vamos detalhar um pouco mais cada uma das interfaces:

- **O1:** 
  - Gerencia todas as Funções de Rede (NFs) da O-RAN, exceto O-RU, para um framework SMO autorizado;
  - 


