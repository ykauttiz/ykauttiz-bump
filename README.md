<div align="center">

<br/>

<img src="https://img.shields.io/badge/yKauttizBump-Bot%20de%20Bump%20Automático-57F287?style=for-the-badge&labelColor=0d0d0d"/>

<br/><br/>

<img src="https://img.shields.io/badge/STATUS-ESTÁVEL-57F287?style=for-the-badge&labelColor=0d0d0d"/>
<img src="https://img.shields.io/badge/LICENÇA-PROPRIETÁRIA-ED4245?style=for-the-badge&labelColor=0d0d0d"/>
<img src="https://img.shields.io/badge/NODE.JS-≥%2018.0.0-339933?style=for-the-badge&logo=nodedotjs&logoColor=white&labelColor=0d0d0d"/>
<img src="https://img.shields.io/badge/SUPORTE-DISCORD-5865F2?style=for-the-badge&logo=discord&logoColor=white&labelColor=0d0d0d"/>
<img src="https://img.shields.io/badge/PREÇO-R%24%2020,00-FEE75C?style=for-the-badge&labelColor=0d0d0d"/>

<br/><br/>

```
╔══════════════════════════════════════════════════════╗
║           yKauttizBump — Auto Bump Bot               ║
║  © yKauttiz — Todos os direitos reservados.          ║
║  Software pago. Redistribuição proibida.              ║
║  Suporte: discord.gg/PXBrrv9aGE                      ║
╚══════════════════════════════════════════════════════╝
```

**Bot de bump automático para o Disboard — multi-conta, jitter gaussiano anti-detecção,
webhook Discord, logs profissionais e setup em 3 minutos.**

[**→ Obter Acesso — R$ 20,00**](https://discord.gg/PXBrrv9aGE) &nbsp;·&nbsp;
[**→ Suporte**](https://discord.gg/PXBrrv9aGE) &nbsp;·&nbsp;
[**→ Updates privados**](https://discord.gg/PXBrrv9aGE)

</div>

---

## ⚠️ Aviso Importante

> Este software opera como **selfbot** — usa um token de conta de usuário comum para automação,
> o que **viola os Termos de Serviço do Discord**.
> O uso é de **inteira responsabilidade do cliente**.
> yKauttiz não se responsabiliza por banimentos ou penalidades.
> **Use exclusivamente em contas secundárias.**

---

## O que é o yKauttizBump

Automatiza o bump do seu servidor no **Disboard** — a maior plataforma de listing de servidores Discord — sem você precisar fazer nada manualmente.

**Por que pagar R$ 20,00?**

Bots gratuitos usam delay fixo (facilmente detectável), não têm retry, travam silenciosamente e não confirmam se o bump funcionou. O yKauttizBump foi construído para ser confiável, discreto e simples de usar.

---

## Funcionalidades

**🎲 Jitter gaussiano anti-detecção**
Todos os delays usam distribuição gaussiana (Box-Muller) com variação de ±5–15%. Nenhum intervalo é igual — o bot imita comportamento humano e não cria padrão detectável.

**✅ Confirmação real de bump**
Após enviar o comando, o bot escuta a resposta do Disboard por até 15 segundos. Se confirmado, registra sucesso. Se não chegar, ainda contabiliza o envio.

**👥 Multi-conta**
Adicione quantas contas quiser. Cada conta tem cooldown rastreado individualmente por token.

**📡 Webhook Discord**
Configure um webhook e receba embed no seu canal a cada bump — com conta, horário e status.

**📂 Log em arquivo**
Ative `LOG_FILE=true` e os logs são salvos em `logs/bump-YYYY-MM-DD.log` com rotação diária.

**🔄 Hot-reload de config**
Edite o `config.json` e execute `kill -USR2 <PID>` — config recarregado sem parar o bot.

**🛡️ Graceful shutdown**
`Ctrl+C` aguarda o ciclo atual, imprime as estatísticas finais e encerra limpo.

**📊 Estatísticas detalhadas**
Taxa de sucesso por conta, uptime, duração do ciclo, último erro. Use `kill -USR1 <PID>` a qualquer momento.

---

## Estrutura de Arquivos

```
yKauttizBump/
├── index.js              ← Ponto de entrada — rode com: node index.js
├── config.json           ← EDITE AQUI: suas contas e configurações
├── .env.example          ← Copie para .env e ajuste se necessário
├── package.json
├── .gitignore
├── services/
│   ├── bumper.js         ← Lógica principal de bump (retry + confirmação)
│   ├── monitor.js        ← Estatísticas e monitoramento
│   ├── serverJoin.js     ← Auto-join do servidor de suporte
│   └── webhook.js        ← Notificações Discord
└── utils/
    ├── logger.js         ← Logs coloridos com suporte a arquivo
    ├── rateLimiter.js    ← Cooldown por token com jitter gaussiano
    ├── shutdown.js       ← Graceful shutdown (SIGINT, SIGTERM, SIGHUP)
    └── validator.js      ← Validação do config.json com mensagens claras
```

---

## Instalação

**Requisito:** Node.js 18 ou superior — [nodejs.org](https://nodejs.org)

**1. Instale as dependências**

```bash
npm install
```

**2. Configure o `config.json`**

Abra o arquivo `config.json` e preencha com seus dados:

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
    "timeout":              35000,
    "webhookUrl":           null
  }
}
```

Para usar **múltiplas contas**, adicione mais objetos no array `accounts`.

**3. (Opcional) Configure o `.env`**

```bash
cp .env.example .env
```

**4. Inicie**

```bash
node index.js
```

---

## Referência Completa — config.json

| Campo | Tipo | Padrão | Descrição |
|-------|------|--------|-----------|
| `accounts[].token` | string | — | Token da conta Discord |
| `accounts[].channelId` | string | — | ID do canal de bump (só números) |
| `accounts[].label` | string | `""` | Nome amigável nos logs |
| `settings.bumpInterval` | number | `8100000` | Intervalo entre ciclos em ms (135 min = cooldown Disboard) |
| `settings.delayBetweenAccounts` | number | `5000` | Delay entre contas em ms |
| `settings.maxRetries` | number | `3` | Tentativas por falha |
| `settings.retryDelay` | number | `30000` | Espera entre tentativas em ms |
| `settings.timeout` | number | `35000` | Timeout de cada operação em ms |
| `settings.webhookUrl` | string\|null | `null` | URL de webhook para notificações |

## Referência Completa — .env

| Variável | Padrão | Descrição |
|----------|--------|-----------|
| `LOG_LEVEL` | `info` | Nível de log: `debug` \| `info` \| `warn` \| `error` |
| `LOG_FILE` | `false` | `true` para salvar logs em arquivo |
| `WEBHOOK_URL` | — | Alternativa ao `webhookUrl` do config |
| `DEBUG` | `false` | Logs detalhados de depuração |

---

## Como Obter o Token Discord

> ⚠️ Nunca compartilhe seu token. Acesso total à conta.

1. Abra o Discord no **navegador** (não no app desktop)
2. Pressione `F12` → aba **Network**
3. Filtre por `api/v9`
4. Troque de canal ou envie qualquer mensagem
5. Clique em qualquer request → procure o header **`Authorization`**

---

## Comandos

| Ação | Comando |
|------|---------|
| Iniciar o bot | `node index.js` |
| Encerrar (gracioso) | `Ctrl+C` |
| Ver estatísticas | `kill -USR1 $(pgrep -f index.js)` |
| Recarregar config | `kill -USR2 $(pgrep -f index.js)` |

---

## Solução de Problemas

| Problema | Causa Provável | Solução |
|----------|---------------|---------|
| `Login falhou` | Token inválido ou expirado | Gere um novo token |
| `Canal não encontrado` | channelId errado | Verifique o ID — deve ter 17-20 dígitos |
| `Cooldown ativo` | Bump muito recente | Aguarde o intervalo configurado |
| `Timeout após Xs` | Conexão lenta | Aumente `timeout` no config.json |
| `Todas as tentativas falharam` | Disboard offline ou sem permissão | Verifique se o Disboard está no servidor |

---

## Suporte e Atualizações

Todo o suporte é feito **exclusivamente via Discord**.

Novas versões são distribuídas em um **canal privado exclusivo para clientes** — você recebe notificação assim que uma atualização estiver disponível. Sem necessidade de baixar nada manualmente.

**Servidor oficial:** [discord.gg/PXBrrv9aGE](https://discord.gg/PXBrrv9aGE)

---

<br/>

<div align="center">

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                                                                              ║
║                    © yKauttiz — TODOS OS DIREITOS RESERVADOS                 ║
║                                                                              ║
║   Este software é propriedade exclusiva de yKauttiz e está protegido por    ║
║   direitos autorais. A licença concedida ao cliente é pessoal,               ║
║   intransferível e não exclusiva.                                            ║
║                                                                              ║
║   ✗  Proibido redistribuir, compartilhar ou revender                         ║
║   ✗  Proibido remover ou alterar avisos de copyright                         ║
║   ✗  Proibido criar versões derivadas sem autorização escrita                ║
║   ✗  Proibido usar como base para outros projetos                            ║
║   ✗  Proibido contornar qualquer proteção do software                        ║
║                                                                              ║
║   ✓  Uso pessoal pelo cliente licenciado                                     ║
║   ✓  Execução em suas próprias contas autorizadas                            ║
║                                                                              ║
║   Versões legítimas SEMPRE contêm: yKauttiz · discord.gg/PXBrrv9aGE         ║
║                                                                              ║
║   Violações estão sujeitas a medidas legais.                                 ║
║                                                                              ║
║   discord.gg/PXBrrv9aGE  ·  Servidor ID: 1356778105737580554                ║
║                                                                              ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

Feito com 💜 por **yKauttiz** · [discord.gg/PXBrrv9aGE](https://discord.gg/PXBrrv9aGE)

</div>
