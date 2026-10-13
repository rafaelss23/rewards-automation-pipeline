# README

# 🚀 Rewards & People Analytics Pipeline - Zup Innovation

Este repositório contém uma solução integrada de **People Analytics & Automação de Processos** desenvolvida para a área de **Rewards (Remuneração e Benefícios)**.

O projeto simula um ecossistema completo end-to-end: tratamento de dados de colaboradores, cálculo de competitividade salarial (**Compa-Ratio**), monitoramento executivo via **Power BI** e orquestração de fluxos de aprovação com **n8n**.

---

## 🏗️ Arquitetura da Solução

```mermaid
graph TD
A[📝 Form Trigger: Solicitação de Ajuste] –>|Dados do Zupper| B(⚙️ n8n: Orquestrador)
B –>|Validação Salarial <= R$ 15.000| C{Validador If}
C –>|Sim / Aprovado| D[📧 Send Email: Notificação de Sucesso]
C –>|Não / Exceção| E[⚠️ Send Email: Alerta de Análise RH]
F[(📊 Excel: Base tb_Rewards)] –>|Importação Modelo Star Schema| G[💻 Power BI: Dashboard Executivo]

**📂 Módulos do Projeto
1. Módulo Excel & Engenharia de Dados (`/data`)**
• Base de dados simulando **150 Zuppers** em áreas cruciais (Engenharia, Data & AI, Produto, Design e Rewards).
• Criação de regras de negócio de RH:
    ◦ **Compa-Ratio:** $(\text{Salário Atual} / \text{Midpoint de Mercado})$.
    ◦ **Status de Enquadramento:** Alertas para salários abaixo do piso ($< 85\%$) e acima do teto ($> 115\%$).

**2. Módulo Power BI (`/powerbi`)**
• **Modelagem Star Schema:** Separação entre tabela Fato (`tb_Rewards`) e Dimensão (`dCargos`).
• **Medidas DAX:** Métricas de Headcount, Custo Total de Pessoas, Folha Salarial e Compa-Ratio Médio.
• **UX/UI:** Formatação condicional para rápida identificação de riscos de turnover e discrepâncias orçamentárias.

**3. Módulo n8n & Automação (`/n8n`)**
• Workflow orquestrado no **n8n** rodando via container Docker.
• **Form Trigger:** Captura de solicitações de alteração salarial.
• **If Node:** Regra de negócio automatizada para aprovações diretas $\le R\$ 15.000,00$.
• **Send Email:** Notificações dinâmicas para o solicitante e alertas de exceção para o time de Rewards.

**🛠️ Tecnologias Utilizadas**
• **Orquestração Low-Code:** n8n (Docker)
• **Visualização de Dados:** Power BI & DAX
• **Manipulação de Dados:** Excel / Python (Pandas)
• **Versionamento & Governança:** Git & GitHub

**🚀 Como Executar o Workflow do n8n**
1. Baixe o arquivo `workflow_rewards.json` localizado na pasta `/n8n`.
2. No seu n8n local, clique em **Workflows** -> **Import from File**.
3. Selecione o arquivo e execute as conexões necessárias.
