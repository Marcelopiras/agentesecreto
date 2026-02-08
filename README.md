# agentesecreto
🕵️ Agente Secreto - Bot de Análise Política e Fact-Checking
# 🕵️ Agente Secreto - Bot de Análise Política e Fact-Checking

![n8n](https://img.shields.io/badge/n8n-Workflow-orange?style=flat-square&logo=n8n)
![Postgres](https://img.shields.io/badge/PostgreSQL-Database-blue?style=flat-square&logo=postgresql)
![DeepSeek](https://img.shields.io/badge/AI-DeepSeek_V3-blueviolet?style=flat-square)

Um fluxo automatizado no **n8n** que monitora notícias políticas em tempo real, utiliza Inteligência Artificial para investigar a veracidade dos fatos e envia relatórios executivos via WhatsApp.

## 🚀 Funcionalidades

- **📡 Monitoramento RSS:** Coleta notícias do Google News (Governo, Congresso, Ministros).
- **🧠 IA Investigativa:** Utiliza o modelo **DeepSeek** com uma persona de "Agente Secreto" para análise forense digital.
- **🔍 Checagem de Fatos:** A IA possui acesso a ferramentas de busca para validar informações antes de emitir um veredito.
- **🗄️ Banco de Dados SQL:** Salva histórico, evita duplicidade de notícias e gerencia fila de análise.
- **📱 Notificações WhatsApp:** Envia o resumo, veredito (Verdadeiro/Falso/Inconclusivo) e link da fonte via **Evolution API**.
- **🔄 Ciclo Inteligente:** Sistema de loop que respeita limites de taxa (rate limits) e processa notícias em lotes.

## 🛠️ Arquitetura do Fluxo

```mermaid
graph TD
    RSS[Coleta RSS] --> Filtro[Filtro & Deduplicação]
    Filtro --> Banco[(PostgreSQL)]
    Banco -->|Select Pendentes| Loop{Loop de Processamento}
    Loop --> IA[Agente Secreto IA]
    IA --> Zap[Envio WhatsApp]
    Zap --> Update[Atualiza Status DB]
    Update --> Loop
