<div align="center">

<img src="https://img.shields.io/badge/vers%C3%A3o-3.0.0-57F287?style=for-the-badge&labelColor=0d0d0d" />
<img src="https://img.shields.io/badge/node-%3E%3D18.0.0-5865F2?style=for-the-badge&logo=node.js&labelColor=0d0d0d" />
<img src="https://img.shields.io/badge/software-pago-ED4245?style=for-the-badge&labelColor=0d0d0d" />
<img src="https://img.shields.io/badge/discord-yKauttiz-5865F2?style=for-the-badge&logo=discord&labelColor=0d0d0d" />
<img src="https://img.shields.io/badge/⚠%20use%20por%20sua%20conta%20e%20risco-ED4245?style=for-the-badge&labelColor=0d0d0d" />

<br/><br/>

```
╔══════════════════════════════════════════════════════════════╗
║         yKauttizBump  —  Auto Bump Bot  v3.0.0               ║
╠══════════════════════════════════════════════════════════════╣
║  © 2025 yKauttiz — Todos os direitos reservados.            ║
║  Software pago. Uso não autorizado é estritamente proibido.  ║
╠══════════════════════════════════════════════════════════════╣
║  Discord : yKauttiz                                          ║
║  Servidor : https://discord.gg/PXBrrv9aGE                   ║
╚══════════════════════════════════════════════════════════════╝
```

**Bot de bump automático para Discord com suporte a múltiplas contas, múltiplos bots, jitter gaussiano, confirmação de bump, webhook e logs em arquivo.**

[discord.gg/PXBrrv9aGE](https://discord.gg/PXBrrv9aGE) · © 2025 yKauttiz

</div>

---

## ⚠️ Aviso Importante

> **USE POR SUA CONTA E RISCO.**
> Este software utiliza uma conta de usuário comum (selfbot) para enviar comandos slash — o que viola os Termos de Serviço do Discord.
> yKauttiz **não** se responsabiliza por banimentos, suspensões ou qualquer consequência.
> Recomenda-se uso exclusivo em contas secundárias ou de teste.

---

## ✨ O que há de novo na v3.0.0

| # | Feature | Descrição |
|---|---------|-----------|
| 🔧 | **Multi-bot** | Suporte a Disboard, Bump.top, DiscordServers e Disforge simultaneamente |
| 💬 | **Confirmação de bump** | Escuta a resposta real do bot para confirmar que o bump foi aceito |
| 📡 | **Webhook** | Notificações em canal Discord após cada bump (sucesso ou falha) |
| 🎲 | **Jitter gaussiano** | Delays com distribuição gaussiana em 3 níveis — cooldown, retry e inter-conta |
| 🏷️ | **Labels de conta** | Nomeie cada conta no config para logs mais legíveis |
| 📂 | **Log em arquivo** | `LOG_FILE=true` salva todos os logs em `logs/bump-YYYY-MM-DD.log` |
| 🔄 | **Hot-reload** | `kill -USR2 <pid>` recarrega o config sem parar o bot |
| 🖥️ | **Servidor de suporte** | Entra automaticamente em discord.gg/PXBrrv9aGE ao iniciar |
| 📊 | **Estatísticas por bot** | Monitor mostra sucessos separados por bot de bump |

---

## 📋 Bots Suportados

| Bot | ID | Comando | Status |
|-----|----|---------|--------|
| **Disboard** | `302050872383242240` | `/bump` | ✅ Estável |
| **Bump.top** | `735147814878969968` | `/bump` | ✅ Estável |
| **DiscordServers** | `476303446547792897` | `/bump` | ✅ Estável |
| **Disforge** | `1109580315529682954` | `/bump` | ✅ Estável |

Configure quais bots usar em `config.json → settings.bumpBots`.

---

## 📁 Estrutura do Projeto

```
yKauttizBump/
├── index.js                   ← Entry point principal
├── config.json                ← Configuração de contas e settings
├── .env.example               ← Template de variáveis de ambiente
├── package.json
├── services/
│   ├── bumpService.js         ← Lógica de bump (multi-bot + retry + confirmação)
│   ├── monitorService.js      ← Estatísticas e monitoramento
│   ├── webhookService.js      ← Notificações via webhook Discord
│   └── serverJoinService.js   ← Auto-join do servidor de suporte
└── utils/
    ├── configManager.js       ← Carregamento e merge de configuração
    ├── logger.js              ← Logger colorido + log em arquivo
    ├── rateLimiter.js         ← Cooldown por token com jitter gaussiano
    ├── shutdownHandler.js     ← Graceful shutdown (SIGINT, SIGTERM, SIGHUP)
    └── validator.js           ← Validação de config e environment
```

---

## 🚀 Instalação

### Pré-requisitos

- **Node.js 18+** — [nodejs.org](https://nodejs.org)
- Uma **conta Discord secundária** (não use sua conta principal)
- O bot de bump adicionado no servidor e o canal de bump identificado

### Passo a Passo

**1. Clone ou baixe o repositório**

```bash
git clone https://github.com/ykauttiz/ykauttiz-bump
cd ykauttiz-bump
```

**2. Instale as dependências**

```bash
npm install
```

**3. Configure o `config.json`**

Abra `config.json` e substitua os valores padrão:

```json
{
  "accounts": [
    {
      "token":     "SEU_TOKEN_DISCORD_AQUI",
      "channelId": "ID_DO_CANAL_DE_BUMP",
      "label":     "conta-principal"
    }
  ],
  "settings": {
    "bumpInterval":          8100000,
    "delayBetweenAccounts":  5000,
    "maxRetries":            3,
    "retryDelay":            30000,
    "timeout":               30000,
    "confirmationTimeout":   15000,
    "bumpBots":              ["disboard"],
    "webhookUrl":            null
  }
}
```

**4. (Opcional) Configure o `.env`**

```bash
cp .env.example .env
```

Edite o `.env` se quiser ajustar `LOG_LEVEL`, ativar `LOG_FILE=true` ou adicionar um `WEBHOOK_URL`.

**5. Inicie o bot**

```bash
npm start
```

---

## 🔑 Como obter o token Discord

> ⚠️ Nunca compartilhe seu token. Quem tiver o token tem acesso total à conta.

1. Abra o Discord no **navegador** (não no app)
2. Pressione `F12` para abrir o DevTools
3. Vá na aba **Network**
4. Filtre por `api/v9`
5. Faça qualquer ação no Discord (enviar mensagem, trocar de canal)
6. Clique em qualquer request e procure o header `Authorization` — esse é seu token

---

## ⚙️ Configuração Completa

### `config.json` — Referência

| Campo | Tipo | Padrão | Descrição |
|-------|------|--------|-----------|
| `accounts[].token` | string | — | Token da conta Discord |
| `accounts[].channelId` | string | — | ID do canal de bump |
| `accounts[].label` | string | `""` | Nome amigável para logs |
| `settings.bumpInterval` | number | `8100000` | Intervalo entre ciclos (ms) |
| `settings.delayBetweenAccounts` | number | `5000` | Delay entre contas (ms) |
| `settings.maxRetries` | number | `3` | Tentativas por falha |
| `settings.retryDelay` | number | `30000` | Espera entre tentativas (ms) |
| `settings.timeout` | number | `30000` | Timeout de operação (ms) |
| `settings.confirmationTimeout` | number | `15000` | Timeout de confirmação do bot (ms) |
| `settings.bumpBots` | string[] | `["disboard"]` | Bots a usar: `disboard`, `bumptop`, `discordservers`, `disforge` |
| `settings.webhookUrl` | string\|null | `null` | URL de webhook para notificações |

### Variáveis de Ambiente — Referência

Variáveis de ambiente **sobrescrevem** os valores do `config.json`.

| Variável | Padrão | Descrição |
|----------|--------|-----------|
| `DISCORD_TOKEN` | — | Token de conta única (substitui config.json) |
| `DISCORD_CHANNEL_ID` | — | Canal de conta única |
| `DISCORD_LABEL` | `conta-env` | Label da conta via env |
| `DEBUG` | `false` | Logs detalhados de depuração |
| `LOG_LEVEL` | `info` | `debug` \| `info` \| `warn` \| `error` |
| `LOG_FILE` | `false` | Salvar logs em arquivo |
| `BUMP_INTERVAL` | `8100000` | Sobrescreve `bumpInterval` |
| `DELAY_BETWEEN_ACCOUNTS` | `5000` | Sobrescreve `delayBetweenAccounts` |
| `MAX_RETRIES` | `3` | Sobrescreve `maxRetries` |
| `RETRY_DELAY` | `30000` | Sobrescreve `retryDelay` |
| `TIMEOUT` | `30000` | Sobrescreve `timeout` |
| `CONFIRMATION_TIMEOUT` | `15000` | Sobrescreve `confirmationTimeout` |
| `WEBHOOK_URL` | — | URL de webhook |

---

## 📊 Comandos de Processo

Com o bot rodando, você pode enviar sinais sem parar o processo:

| Comando | Ação |
|---------|------|
| `npm run stats` | Imprime estatísticas no terminal |
| `npm run reload` | Recarrega o `config.json` sem reiniciar |
| `Ctrl+C` | Encerra o bot graciosamente (imprime stats antes de sair) |

---

## 🔔 Webhook — Notificações

Configure `webhookUrl` no `config.json` ou via `WEBHOOK_URL` no `.env` para receber notificações em um canal Discord após cada bump:

- ✅ **Bump realizado** — conta, bots usados e horário
- ❌ **Bump falhou** — conta, motivo do erro e horário

---

## 📝 Exemplo de Output

```
╔══════════════════════════════════════════════════════════════╗
║         yKauttizBump  —  Auto Bump Bot  v3.0.0               ║
╚══════════════════════════════════════════════════════════════╝

[12:00:00] [INFO]  Verificando associação ao servidor de suporte...
[12:00:02] [OK]    Servidor de suporte: já membro ✓
[12:00:02] [INFO]  Iniciado com 2 conta(s) | Bots: disboard
[12:00:02] [INFO]  Configurações: Intervalo=135min | Delay=5s | Retries=3
  ──────────────────────────────────────────────────────────────
[12:00:02] [INFO]  🔄 Ciclo #1 — 01/01/2025 12:00:02
[12:00:02] [INFO]  👤 Processando conta: conta-1 (TOKEN123...)
[12:00:05] [OK]    Bump concluído! Conta: conta-1 | Bots: Disboard
[12:00:10] [INFO]  👤 Processando conta: conta-2 (TOKEN456...)
[12:00:13] [OK]    Bump concluído! Conta: conta-2 | Bots: Disboard
  ──────────────────────────────────────────────────────────────

  📊  yKauttizBump v3.0.0 — Estatísticas
  ────────────────────────────────────────────────────────────
  Uptime             : 0h 0m 15s
  Ciclos concluídos  : 1
  Total de tentativas: 2
  Sucessos           : 2
  Taxa de sucesso    : 100.0%

  Por conta:
    TOKEN123...  →  1/1 (100%) [Disboard] último: 12:00:05
    TOKEN456...  →  1/1 (100%) [Disboard] último: 12:00:13

[12:00:15] [INFO]  ✅ Ciclo #1 concluído. Próximo bump em ~135 minuto(s)...
```

---

## ❓ Erros Comuns

| Erro | Causa | Solução |
|------|-------|---------|
| `Login falhou` | Token inválido ou expirado | Obtenha um novo token |
| `Canal não encontrado` | channelId errado ou sem acesso | Verifique o ID e as permissões |
| `Cooldown ativo` | Bump feito há pouco tempo | Aguarde o intervalo configurado |
| `Timeout` | Conexão lenta ou Discord instável | Aumente `timeout` no config |
| `Todas as tentativas falharam` | Bot de bump offline ou sem permissão | Verifique se o bot está no servidor |

---

## 📜 Histórico de Versões

| Versão | Status | Novidades |
|--------|--------|-----------|
| **v3.0.0** | ✅ Atual | Multi-bot, confirmação de bump, webhook, jitter gaussiano, labels, log em arquivo, hot-reload |
| v2.0.0 | ⚠️ Legacy | Retry automático, graceful shutdown, rate limiter |
| v1.0.0 | 🔴 Obsoleto | Versão inicial |

---

## 📄 Copyright & Licença

```
© 2025 yKauttiz · Todos os direitos reservados
discord.gg/PXBrrv9aGE · Servidor ID: 1356778105737580554
```

- ✅ Uso pessoal permitido (compradores autorizados)
- ❌ Proibido redistribuir, revender ou compartilhar
- ❌ Proibido remover autoria ou avisos de copyright
- ❌ Proibido criar forks públicos sem autorização

Versões legítimas sempre contêm: `yKauttiz` · `discord.gg/PXBrrv9aGE`

---

<div align="center">

Feito com 💜 por **yKauttiz** · [discord.gg/PXBrrv9aGE](https://discord.gg/PXBrrv9aGE)

</div>
