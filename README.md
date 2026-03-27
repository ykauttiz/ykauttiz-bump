<div align="center">

<br/>

```
██╗   ██╗██╗  ██╗ █████╗ ██╗   ██╗████████╗████████╗██╗███████╗    ██████╗ ██╗   ██╗███╗   ███╗██████╗
╚██╗ ██╔╝██║ ██╔╝██╔══██╗██║   ██║╚══██╔══╝╚══██╔══╝██║╚══███╔╝    ██╔══██╗██║   ██║████╗ ████║██╔══██╗
 ╚████╔╝ █████╔╝ ███████║██║   ██║   ██║      ██║   ██║  ███╔╝     ██████╔╝██║   ██║██╔████╔██║██████╔╝
  ╚██╔╝  ██╔═██╗ ██╔══██║██║   ██║   ██║      ██║   ██║ ███╔╝      ██╔══██╗██║   ██║██║╚██╔╝██║██╔═══╝
   ██║   ██║  ██╗██║  ██║╚██████╔╝   ██║      ██║   ██║███████╗    ██████╔╝╚██████╔╝██║ ╚═╝ ██║██║
   ╚═╝   ╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝    ╚═╝      ╚═╝   ╚═╝╚══════╝    ╚═════╝  ╚═════╝ ╚═╝     ╚═╝╚═╝
```

<img src="https://img.shields.io/badge/STATUS-ESTÁVEL-57F287?style=for-the-badge&labelColor=0d0d0d"/>
<img src="https://img.shields.io/badge/LICENÇA-PROPRIETÁRIA-ED4245?style=for-the-badge&labelColor=0d0d0d"/>
<img src="https://img.shields.io/badge/NODE-≥%2018.0.0-5865F2?style=for-the-badge&logo=node.js&logoColor=white&labelColor=0d0d0d"/>
<img src="https://img.shields.io/badge/SUPORTE-DISCORD-5865F2?style=for-the-badge&logo=discord&logoColor=white&labelColor=0d0d0d"/>

<br/><br/>

> **Bot de bump automático para Discord.**
> Multi-conta · 6 bots de listing · Jitter anti-detecção · Webhook · Logs profissionais.

**[→ Obter acesso](https://discord.gg/PXBrrv9aGE)** · **[→ Suporte](https://discord.gg/PXBrrv9aGE)** · **[→ Updates](https://discord.gg/PXBrrv9aGE)**

</div>

---

## ⚠️ Aviso Legal

> Este software opera como **selfbot** — utiliza tokens de contas de usuário comuns para automação, o que **viola os Termos de Serviço do Discord**.
> O uso é de **inteira responsabilidade do cliente**. yKauttiz não se responsabiliza por banimentos, suspensões ou qualquer penalidade aplicada pelo Discord.
> **Recomendamos fortemente o uso exclusivo em contas secundárias.**

---

## O que é o yKauttizBump

O **yKauttizBump** automatiza o bump do seu servidor em até **6 plataformas de listing** simultaneamente, com múltiplas contas, delays com distribuição gaussiana para anti-detecção, confirmação real de bump por resposta do bot, notificações via webhook e logs salvos em arquivo.

Enquanto a maioria dos bots gratuitos faz bump apenas no Disboard com delay fixo e sem qualquer proteção, o yKauttizBump foi construído para ser **discreto, confiável e profissional**.

---

## Bots de Listing Suportados

| Bot | Plataforma | Cooldown | Status |
|-----|-----------|---------|--------|
| **Disboard** | disboard.org | 135 min | ✅ Suportado |
| **Bump.top** | bump.top | 60 min | ✅ Suportado |
| **DiscordServers** | discordservers.com | 120 min | ✅ Suportado |
| **Disforge** | disforge.com | 60 min | ✅ Suportado |
| **Infinity List** | infinitybots.gg | 120 min | ✅ Suportado |
| **Blist** | blist.xyz | 120 min | ✅ Suportado |

Configure quais bots usar em `config.json → settings.bumpBots`. Você pode usar múltiplos ao mesmo tempo.

---

## Diferenciais

**Jitter gaussiano em todos os delays**
Nenhum intervalo é fixo. Cada sleep usa distribuição Box-Muller com ±5–15% de variação — o timing imita comportamento humano e não cria fingerprint de sessão.

**Confirmação real de bump**
Após enviar o comando slash, o bot escuta a mensagem de resposta do bot de listing. Se confirmado, registra o sucesso. Se não chegar em 15s, contabiliza como enviado mesmo assim (o comando pode ter funcionado sem resposta visível).

**Multi-conta com delay jitterizado**
Adicione quantas contas quiser. Cada conta tem seu próprio cooldown rastreado por token. O delay entre contas também é gaussiano.

**Hot-reload sem downtime**
Edite o `config.json` e mande `kill -USR2 <PID>` — o config é recarregado sem parar o bot.

**Webhook Discord**
Configure uma URL de webhook e receba embeds formatados no seu canal a cada bump — sucesso ou falha.

**Log em arquivo**
Ative `LOG_FILE=true` e todos os logs são salvos em `logs/bump-YYYY-MM-DD.log` com rotação diária automática.

---

## Arquivos do Projeto

```
yKauttizBump/
├── index.js              ← Inicie o bot com: node index.js
├── config.json           ← EDITE AQUI: suas contas e configurações
├── .env.example          ← Copie para .env e ajuste se necessário
├── package.json
├── services/
│   ├── bumper.js         ← Lógica de bump (6 bots, retry, confirmação)
│   ├── monitor.js        ← Estatísticas em tempo real
│   ├── serverJoin.js     ← Auto-join do servidor de suporte
│   └── webhook.js        ← Notificações Discord
└── utils/
    ├── logger.js         ← Logs coloridos + arquivo
    ├── rateLimiter.js    ← Cooldown por token com jitter
    ├── shutdown.js       ← Graceful shutdown
    └── validator.js      ← Validação do config.json
```

---

## Instalação

**Requisito:** Node.js versão 18 ou superior — [nodejs.org](https://nodejs.org)

**1. Instale as dependências**

```bash
npm install
```

**2. Configure o `config.json`**

Abra o arquivo `config.json` e preencha:

```json
{
  "accounts": [
    {
      "token":     "SEU_TOKEN_DISCORD_AQUI",
      "channelId": "ID_DO_CANAL_DE_BUMP_AQUI",
      "label":     "minha-conta"
    }
  ],
  "settings": {
    "bumpInterval":         8100000,
    "delayBetweenAccounts": 5000,
    "maxRetries":           3,
    "retryDelay":           30000,
    "timeout":              30000,
    "bumpBots":             ["disboard"],
    "webhookUrl":           null
  }
}
```

Para usar múltiplas contas, adicione mais objetos em `accounts[]`.
Para usar múltiplos bots, adicione ao array: `["disboard", "bumptop", "discordservers"]`.

**3. (Opcional) Configure o `.env`**

```bash
cp .env.example .env
```

Edite o `.env` para ajustar o nível de log, ativar log em arquivo ou adicionar webhook.

**4. Inicie**

```bash
node index.js
```

---

## Referência de Configuração

### config.json

| Campo | Tipo | Padrão | Descrição |
|-------|------|--------|-----------|
| `accounts[].token` | string | — | Token da conta Discord |
| `accounts[].channelId` | string | — | ID do canal onde o bump é feito |
| `accounts[].label` | string | `""` | Nome para identificação nos logs |
| `settings.bumpInterval` | number | `8100000` | Intervalo entre ciclos em ms (135 min) |
| `settings.delayBetweenAccounts` | number | `5000` | Delay entre contas em ms |
| `settings.maxRetries` | number | `3` | Tentativas por falha |
| `settings.retryDelay` | number | `30000` | Espera entre tentativas em ms |
| `settings.timeout` | number | `30000` | Timeout de cada operação em ms |
| `settings.bumpBots` | string[] | `["disboard"]` | Bots a usar |
| `settings.webhookUrl` | string\|null | `null` | URL de webhook para notificações |

**Valores válidos para `bumpBots`:** `disboard`, `bumptop`, `discordservers`, `disforge`, `infinity`, `blist`

### .env

| Variável | Padrão | Descrição |
|----------|--------|-----------|
| `LOG_LEVEL` | `info` | `debug` \| `info` \| `warn` \| `error` |
| `LOG_FILE` | `false` | `true` para salvar logs em arquivo |
| `WEBHOOK_URL` | — | URL de webhook (alternativa ao config.json) |
| `DEBUG` | `false` | Logs detalhados de depuração |

---

## Como obter o token Discord

> ⚠️ Nunca compartilhe seu token. Quem tiver o token tem **acesso total** à conta.

1. Abra o Discord no **navegador** (não no app)
2. Pressione `F12` → aba **Network**
3. Filtre por `api/v9`
4. Troque de canal ou envie uma mensagem
5. Clique em qualquer request → procure o header `Authorization`

---

## Comandos Úteis

| Comando | Descrição |
|---------|-----------|
| `node index.js` | Inicia o bot |
| `Ctrl+C` | Encerra graciosamente (imprime estatísticas) |
| `kill -USR1 <PID>` | Imprime estatísticas sem parar |
| `kill -USR2 <PID>` | Recarrega o config.json sem parar |

---

## Solução de Problemas

| Problema | Causa | Solução |
|----------|-------|---------|
| `Login falhou` | Token inválido ou expirado | Obtenha um novo token |
| `Canal não encontrado` | channelId errado ou sem acesso | Verifique o ID e as permissões |
| `Cooldown ativo` | Bump feito há pouco tempo | Aguarde o intervalo configurado |
| `Timeout` | Conexão lenta ou Discord instável | Aumente `timeout` no config |
| `Bot inválido` | Nome de bot com erro de digitação | Use exatamente: `disboard`, `bumptop`, etc. |

---

## Suporte e Atualizações

Todo o suporte é prestado **exclusivamente pelo Discord**.

As atualizações são distribuídas automaticamente em um **canal privado para clientes** no servidor — sem necessidade de baixar nada manualmente. Você será notificado no canal assim que uma nova versão estiver disponível.

**Servidor oficial:** [discord.gg/PXBrrv9aGE](https://discord.gg/PXBrrv9aGE)

---

## Copyright e Licença

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                                                                              ║
║   yKauttizBump — Auto Bump Bot para Discord                                  ║
║   © yKauttiz. Todos os direitos reservados.                                  ║
║                                                                              ║
║   Este software é de propriedade exclusiva de yKauttiz e protegido por       ║
║   direitos autorais. A licença é pessoal, intransferível e não exclusiva.    ║
║                                                                              ║
║   É ESTRITAMENTE PROIBIDO:                                                   ║
║     × Redistribuir, compartilhar ou revender este software                   ║
║     × Remover ou alterar avisos de copyright ou autoria                      ║
║     × Criar forks ou versões derivadas sem autorização por escrito           ║
║     × Usar o código como base para outros projetos                           ║
║     × Contornar qualquer mecanismo de proteção ou verificação                ║
║                                                                              ║
║   É PERMITIDO:                                                               ║
║     ✓ Uso pessoal pelo cliente licenciado                                    ║
║     ✓ Executar em seus próprios servidores e contas autorizadas              ║
║                                                                              ║
║   Violações desta licença estão sujeitas a medidas legais cabíveis.         ║
║                                                                              ║
║   Versões legítimas SEMPRE contêm:                                           ║
║     → yKauttiz                                                               ║
║     → discord.gg/PXBrrv9aGE                                                  ║
║                                                                              ║
║   Servidor oficial : discord.gg/PXBrrv9aGE                                  ║
║   Servidor ID      : 1356778105737580554                                     ║
║   Contato          : Discord — yKauttiz                                      ║
║                                                                              ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

<div align="center">

Feito com 💜 por **yKauttiz** · [discord.gg/PXBrrv9aGE](https://discord.gg/PXBrrv9aGE)

</div>
