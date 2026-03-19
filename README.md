# 🏢 Infraestrutura de Rede Corporativa — Segmentação e Segurança L2/L3

Laboratório prático baseado no currículo **CompTIA Network+ (N10-009)**, simulado no Cisco Packet Tracer.

---

## 📖 Sobre o projeto

O cenário simula a modernização de uma rede legada com problemas reais: domínios de broadcast grandes demais, sem segmentação entre departamentos e sem nenhuma proteção nas portas de acesso. O objetivo foi resolver isso na prática, não só na teoria.

---

## 🎯 O que foi implementado

- **VLANs por departamento** — isolar Diretoria, Vendas e Servidores em sub-redes separadas
- **Port-Security** — impedir que dispositivos não autorizados se conectem aos switches de acesso
- **STP (Spanning Tree Protocol)** — evitar loops de rede na topologia
- **Roteamento Inter-VLAN via Switch Core (L3)** — comunicação entre VLANs sem precisar de um roteador dedicado

---

## 🛠️ Endereçamento

| Departamento | VLAN | Rede IP         | Gateway        |
| :----------- | :--- | :-------------- | :------------- |
| Diretoria    | 10   | 192.168.10.0/24 | 192.168.10.1   |
| Vendas       | 20   | 192.168.20.0/24 | 192.168.20.1   |
| Servidores   | 30   | 192.168.30.0/24 | 192.168.30.1   |
| Gestão       | 99   | 192.168.99.0/24 | 192.168.99.1   |
| Blackhole    | 666  | —               | —              |

A VLAN 666 (Blackhole) é usada para jogar portas não utilizadas — qualquer tráfego que cair nela vai a lugar nenhum.

---

## 🗺️ Topologia

> Estrutura hierárquica da rede, com os switches de acesso conectados ao Switch Core central.

<img src="https://github.com/user-attachments/assets/2884d9c7-6527-4663-8627-78b786946065" alt="Diagrama da Topologia" width="800">

---

## Validação

### 🔒 Port-Security funcionando

Conectei um dispositivo não cadastrado na rede para testar. O switch identificou o MAC desconhecido e desativou a porta automaticamente — exatamente o comportamento esperado.

<img src="https://github.com/user-attachments/assets/f71fd54f-9560-4230-8757-698ad63e411a" alt="Evidencia Port-Security" width="800">

### 📡 Conectividade entre VLANs

Com o roteamento L3 configurado, os departamentos conseguem se comunicar normalmente passando pelo Switch Core. Testado via ping e tracert, sem perda de pacotes.

<img src="https://github.com/user-attachments/assets/c425b349-ac7e-467f-ac1c-fa9cd4fe71a7" alt="Evidencia de conectividade" width="800">

---

## 📁 Estrutura do repositório
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

## 📈 Conclusão

O que mais ficou claro durante o lab foi a importância de planejar o endereçamento e as VLANs antes de sair configurando. Um desalinhamento simples na VLAN nativa já é suficiente para gerar alertas de *Native VLAN Mismatch* e desestabilizar o STP. Pequenos detalhes, impacto grande.

No geral, o projeto cobre bem os tópicos de switching, roteamento e segurança que aparecem no Network+.

---

<div align="center">

**Gustavo Percoski**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/gustavo-percoski/)
&nbsp;
[![Gmail](https://img.shields.io/badge/Gmail-000000?style=for-the-badge&logo=gmail&logoColor=white)](mailto:gustavopercoski2@gmail.com)
&nbsp;
[![GitHub](https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/gustavopercoski2-prog)

</div>
