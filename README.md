# 🏢 Infraestrutura de Rede Corporativa: Segmentação e Segurança L2/L3

**Laboratório de Aplicação Prática — Baseado no currículo CompTIA Network+ (N10-009)**

---

## 📖 1. Resumo do Projeto

Este projeto apresenta a implementação de uma rede local (LAN) corporativa simulada no **Cisco Packet Tracer**, com foco na aplicação prática dos conceitos abordados no currículo da certificação **CompTIA Network+ (N10-009)**.

O cenário simula a modernização de uma infraestrutura legada, abordando problemas comuns encontrados em ambientes corporativos, como:

* Domínios de broadcast excessivos
* Falta de segmentação entre departamentos
* Ausência de políticas básicas de segurança em portas de acesso
* Dependência de topologias sem redundância no backbone

A solução proposta utiliza segmentação lógica, hardening de camada 2 e roteamento centralizado em Layer 3 para criar um ambiente **mais seguro, escalável e resiliente**.

---

## 🎯 2. Objetivos de Engenharia

* **Segmentação Lógica (VLANs)**: Isolar departamentos para reduzir broadcast, melhorar desempenho e proteger dados sensíveis.
* **Segurança de Camada 2**: Aplicar políticas de hardening em portas de acesso para mitigar conexões não autorizadas.
* **Resiliência da Topologia**: Implementar Spanning Tree Protocol (STP) com definição manual de Root Bridge para evitar loops.
* **Roteamento Inter-VLAN (Layer 3)**: Centralizar o tráfego em um switch multilayer, reduzindo latência.

---

## 🛠️ 3. Planejamento e Arquitetura

### 3.1. Tabela de Endereçamento IPv4

Foi adotado um esquema de endereçamento privado, priorizando organização e escalabilidade.

| Departamento | VLAN | Rede IP | Gateway | Justificativa Técnica |
| :--- | :--- | :--- | :--- | :--- |
| **Diretoria** | 10 | 192.168.10.0/24 | 192.168.10.1 | Isolamento de tráfego administrativo |
| **Vendas** | 20 | 192.168.20.0/24 | 192.168.20.1 | Maior densidade de hosts operacionais |
| **Servidores** | 30 | 192.168.30.0/24 | 192.168.30.1 | Controle de acesso restrito via ACLs |
| **Gestao** | 99 | 192.168.99.0/24 | 192.168.99.1 | Acesso exclusivo para SSH/VTY e gerência |
| **Blackhole** | 666 | — | — | Segurança: Mitigação de VLAN Hopping |

---

## 🏗️ 3.2. Arquitetura da Topologia

A topologia segue o **modelo hierárquico**, separando funções de acesso e core para melhor desempenho e organização lógica.

<img src="https://github.com/user-attachments/assets/2884d9c7-6527-4663-8627-78b786946065" alt="Diagrama da Topologia" width="800">

**Componentes utilizados:**

* 01 Router (Edge): Simulação de acesso à WAN.
* 01 Switch Multilayer (Core): Roteamento Inter-VLAN e Root Bridge do STP.
* 02 Switches de Acesso: Conexão dos dispositivos finais.

---

## ⚙️ 4. Implementação Técnica

### 4.1. Switching — Camada 2

As configurações de acesso seguem o **princípio do menor privilégio**:

* **Port Security**: Modo *sticky* habilitado; Apenas um endereço MAC permitido; Em caso de violação, estado `shutdown`.
* **Trunking (802.1Q)**: VLANs permitidas explicitamente; VLAN nativa definida como VLAN 666 (blackhole).

---

### 4.2. Inteligência de Rede — Camada 3

O switch multilayer atua como o núcleo lógico da rede:

* **SVIs (Switch Virtual Interfaces)**: Criadas para cada VLAN, permitindo comunicação interdepartamental controlada.

<img src="https://github.com/user-attachments/assets/182cbc72-38ca-496f-b5ad-5a49159c662c" alt="Configuração de VLANs no Switch Core" width="600">

* **Spanning Tree Protocol (STP)**: Prioridade ajustada manualmente para garantir o Core como Root Bridge.

---

## 🧪 5. Validação do Ambiente

Para garantir o correto funcionamento da infraestrutura, foram realizados os seguintes testes práticos:

* **Isolamento de Broadcast**: Confirmação de que ARP e DHCP permanecem restritos às suas respectivas VLANs.
* **Teste de Intrusão Física**: Conexão de dispositivo não autorizado resultou no bloqueio imediato via Port Security.

<img src="https://github.com/user-attachments/assets/f71fd54f-9560-4230-8757-698ad63e411a" alt="Evidencia Port-Security" width="600">

* **Conectividade Inter-VLAN**: Testes de `ping` e `tracert` bem-sucedidos entre usuários e servidores, validando o roteamento Layer 3.

<img src="https://github.com/user-attachments/assets/c425b349-ac7e-467f-ac1c-fa9cd4fe71a7" alt="Evidencia de conectividade" widht="600">

---

## 📁 6. Estrutura do Repositório

```
/topology
 └── projeto_rede_corporativa.pkt

/configs
 ├── core-switch.conf
 ├── access-switch-01.conf
 └── access-switch-02.conf

/docs
 └── Projeto_Rede_Switching_Corporativa.pdf
```

---

## 📈 7. Considerações Finais

A execução deste laboratório reforçou a importância do **planejamento prévio (Pre-Staging)** em ambientes de rede. Durante a implementação, foi possível observar que pequenos desalinhamentos de configuração — como inconsistências na VLAN nativa — podem gerar alertas de *Native VLAN Mismatch* e impactar diretamente a estabilidade do STP.

O projeto consolida conhecimentos essenciais de **switching, roteamento e segurança de rede**, servindo como uma base sólida para ambientes corporativos reais e como evidência prática de domínio dos tópicos abordados na certificação CompTIA Network+.

---

<div align="center">

### Development by *Gustavo Percoski*

*IT Support Technician | Jr. Full Stack Developer*

<a href="https://www.linkedin.com/in/gustavo-percoski/" target="_blank">
<img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white" />
</a>
&nbsp;
<a href="mailto:gustavopercoski2@gmail.com">
<img src="https://img.shields.io/badge/Gmail-000000?style=for-the-badge&logo=gmail&logoColor=white" />
</a>
&nbsp;
<a href="https://github.com/gustavopercoski2-prog" target="_blank">
<img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white" />
</a>

</div>

---
