# Arquitetura O-RAN

A arquitetura pode ser apresentada em diferentes escopos

## Arquitetura em Alto Nível

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

Vamos detalhar um pouco mais algumas das interfaces:

- **O1:** 
  - Gerencia todas as Funções de Rede (NFs) da O-RAN, exceto O-RU, para um framework SMO autorizado;
  - Permite o gerenciamento de NFs individualmente ou em conjunto;
- **Open Fronthaul M-plane:**
  - Conecta SMO e O-RU (O-RAN Radio Unit)
  - Promove suporte no gerenciamento em modo híbrido do O-RU (feita pelas interfaces O1 e o Open Fronthaul);

Podemos destacar também que as funções de rede O-RAN podem ser hospedadas
em um hardware customizado ou na O-Cloud;

As funções de rede (NFs) instânciadas no O-Cloud podem utilizar APIs apresentadas por AAL (Accelerator Abstraction Layer);

---
**OBS: O que é um Accelerator Abstraction Layer (AAL)?**
- É uma camada de abstração que fornece APIs padronizadas para acessar aceleradores de hardware (ex.: GPU, FPGA, SmartNICs, DPU).
- Evita que cada NF tenha que depender de drivers específicos de fornecedores.
- Garante portabilidade dos NFs em diferentes infraestruturas O-Cloud.
---

O Near-RT RIC (Near-Real-Time RAN Intelligent Controller) O-RAN NF fornece serviços de análise da RAN através da interface Y1.
Esses serviços podem ser consumidos por Y1 Consumers.

---

**OBS:** Exemplos de Y1 Consumers são: módulos de análise de tráfego da operadora ou sistemas de planejamento de capacidade,

---

## Arquitetura em Nível Lógico

