# 🚀 Rewards & People Analytics Pipeline - Zup Innovation

Este repositório contém uma solução integrada de **People Analytics & Automação de Processos** desenvolvida para a área de **Rewards (Remuneração e Benefícios)**. 

O projeto simula um ecossistema completo end-to-end: tratamento de dados de colaboradores, cálculo de competitividade salarial (**Compa-Ratio**), monitoramento executivo via **Power BI** e orquestração de fluxos de aprovação com **n8n**.

---

## 🏗️ Arquitetura da Solução

```mermaid
graph TD
    A[📝 Form Trigger: Solicitação de Ajuste] -->|Dados do Zupper| B(⚙️ n8n: Orquestrador)
    B -->|Validação Salarial <= R$ 15.000| C{Validador If}
    C -->|Sim / Aprovado| D[📧 Send Email: Notificação de Sucesso]
    C -->|Não / Exceção| E[⚠️ Send Email: Alerta de Análise RH]
    F[(📊 Excel: Base tb_Rewards)] -->|Importação Modelo Star Schema| G[💻 Power BI: Dashboard Executivo]