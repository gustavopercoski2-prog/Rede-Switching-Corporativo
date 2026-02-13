# 🏢 Infraestrutura de Rede Corporativa: Segmentação e Segurança L2/L3

**Laboratório de Aplicação Prática — Baseado no currículo CompTIA Network+ (N10-009)**

---

## 📖 1. Resumo do Projeto

Este projeto apresenta a implementação de uma rede local (LAN) corporativa simulada no **Cisco Packet Tracer**, com foco na aplicação prática dos conceitos abordados no currículo da certificação **CompTIA Network+ (N10-009)**.

O cenário simula a modernização de uma infraestrutura legada, corrigindo falhas como domínios de broadcast excessivos, falta de segmentação e vulnerabilidades de acesso físico.

---

## 🎯 2. Objetivos de Engenharia

* **Segmentação Lógica (VLANs)**: Isolar departamentos para melhorar o desempenho e proteger dados.
* **Segurança de Camada 2**: Aplicar travas nas portas de acesso para impedir conexões não autorizadas.
* **Resiliência da Topologia**: Configurar o Spanning Tree Protocol (STP) para evitar loops na rede.
* **Roteamento Inter-VLAN (Layer 3)**: Centralizar o tráfego em um switch de alta performance para reduzir a latência.

---

## 🛠️ 3. Planejamento e Arquitetura

### 3.1. Tabela de Endereçamento IPv4

| Departamento | VLAN | Rede IP | Gateway | Justificativa Técnica |
| :--- | :--- | :--- | :--- | :--- |
| **Diretoria** | 10 | 192.168.10.0/24 | 192.168.10.1 | Isolamento administrativo |
| **Vendas** | 20 | 192.168.20.0/24 | 192.168.20.1 | Alta densidade de usuários |
| **Servidores** | 30 | 192.168.30.0/24 | 192.168.30.1 | Controle de acesso restrito |
| **Gestao** | 99 | 192.168.99.0/24 | 192.168.99.1 | Gerenciamento exclusivo |
| **Blackhole** | 666 | — | — | Mitigação de ataques |

---

### 3.2. Arquitetura da Topologia

Abaixo está o mapa visual da rede. Ele demonstra como os computadores dos departamentos estão organizados e conectados aos switches de acesso, que por sua vez se comunicam com o núcleo central (Switch Core) para acessar outras redes e a internet.

> **Mapa da Rede:** Representação visual da estrutura hierárquica e conexões entre os setores.
<img src="https://github.com/user-attachments/assets/2884d9c7-6527-4663-8627-78b786946065" alt="Diagrama da Topologia" width="800">

---

## ⚙️ 4. Implementação Técnica

### 4.1. Switching — Camada 2
As portas de acesso foram configuradas para aceitar apenas dispositivos autorizados (Port-Security). Também foram implementados links **Trunk** para permitir que o tráfego de múltiplas VLANs trafegue entre os switches com segurança.

### 4.2. Inteligência de Rede — Camada 3
O **Switch Core** atua como o ponto central de inteligência, realizando o roteamento entre os departamentos através de interfaces virtuais (SVIs).

> **Configuração de VLANs:** O terminal abaixo confirma que as redes de cada departamento foram criadas e estão operando corretamente no núcleo da rede.
<img src="https://github.com/user-attachments/assets/182cbc72-38ca-496f-b5ad-5a49159c662c" alt="Configuração de VLANs no Switch Core" width="800">

---

## 🧪 5. Validação do Ambiente

### 5.1. Teste de Segurança (Port-Security)
Para validar a proteção, simulamos a conexão de um dispositivo invasor. O switch detectou que o endereço MAC não pertencia à rede autorizada e desativou a porta imediatamente.

> **Flagrante de Bloqueio:** À esquerda, o invasor impedido de se comunicar; à direita, o console do Switch mostrando o status de segurança ativado.
<img src="https://github.com/user-attachments/assets/f71fd54f-9560-4230-8757-698ad63e411a" alt="Evidencia Port-Security" width="800">

### 5.2. Teste de Conectividade (Ping/Tracert)
Este teste comprova que a segmentação não impede o trabalho: os departamentos conseguem alcançar os servidores e o gateway de forma estável, passando pelo roteamento de Camada 3.

> **Caminho dos Dados:** O teste demonstra o sucesso do sinal trafegando entre as sub-redes da empresa sem perdas.
<img src="https://github.com/user-attachments/assets/c425b349-ac7e-467f-ac1c-fa9cd4fe71a7" alt="Evidencia de conectividade" width="800">

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
