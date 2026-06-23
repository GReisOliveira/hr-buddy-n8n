# 🤖 HR Buddy — Agente de RH Inteligente

Assistente virtual de RH desenvolvido com **n8n**, integrando **Google Gemini**, **MySQL** e **Vector Store** para responder dúvidas de funcionários via **Telegram**.

---

## 🏗️ Arquitetura

Telegram → Classificador (Gemini Flash) → Switch → AI Agent → Telegram

↘ Fora do tema → Resposta fixa

### Componentes

- **Classificador de intenção (Gemini Flash):** analisa cada mensagem e classifica em `RH_SIMPLES`, `RH_COMPLEXO` ou `FORA_DO_TEMA` antes de acionar o agente principal — economizando tokens e evitando processamento desnecessário
- **Roteamento inteligente (Switch):** direciona o fluxo baseado na classificação, bloqueando perguntas fora do escopo
- **Banco de dados MySQL:** busca dados personalizados do funcionário como saldo de férias e banco de horas
- **Vector Store + Embeddings:** armazena políticas de RH fragmentadas em chunks para recuperação semântica — equivalente ao pipeline de chunking e splitting feito em Python
- **Memória de sessão:** mantém o contexto da conversa por usuário via chat ID do Telegram

---

## ✅ Resultado

Um agente que responde perguntas de RH 24/7, consultando dados reais do funcionário e políticas da empresa, com controle de custo por classificação prévia das mensagens.

---

## 🚀 Como usar

### Pré-requisitos

- [n8n](https://n8n.io/) (cloud ou self-hosted)
- Conta Google com acesso à API do Gemini
- Banco de dados MySQL
- Bot do Telegram criado via [@BotFather](https://t.me/BotFather)

### Variáveis de ambiente necessárias

| Variável | Descrição |
|---|---|
| `GEMINI_API_KEY` | Chave da API do Google Gemini |
| `MYSQL_HOST` | Host do banco de dados |
| `MYSQL_PORT` | Porta do banco de dados |
| `MYSQL_DATABASE` | Nome do banco de dados |
| `MYSQL_USER` | Usuário do banco |
| `MYSQL_PASSWORD` | Senha do banco |
| `TELEGRAM_BOT_TOKEN` | Token do bot do Telegram |

### Instalação

1. Importe o arquivo `workflow.json` no seu n8n
2. Configure as credenciais (Gemini, MySQL, Telegram)
3. Popule o Vector Store com os documentos de política de RH
4. Ative o workflow e teste via Telegram

---

## 🛠️ Stack

| Ferramenta | Uso |
|---|---|
| n8n | Orquestração do workflow |
| Google Gemini Flash | Classificação de intenção + modelo do agente |
| MySQL | Dados dos funcionários |
| Simple Vector Store | Base de conhecimento de RH |
| Telegram | Interface de chat |
