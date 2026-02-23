# Focus Vault 🛡️

Extensão Chrome (MV3) de modo foco com bloqueio real por whitelist.

## Como funciona

1. **Defina o tempo** — Presets (15/30/60 min) ou custom com confirmação ✅
2. **Configure a whitelist** — Adicione sites que você precisa (domínio inteiro ou URL exata)
3. **Inicie o foco** — Todo site fora da whitelist é bloqueado via `declarativeNetRequest`
4. **Página de bloqueio** — Timer regressivo + frase motivacional + atalhos para sites permitidos
5. **Exceções** — Até 3 por sessão, cada uma com motivo obrigatório

## Instalar (modo desenvolvedor)

1. Abra `chrome://extensions/`
2. Ative "Modo do desenvolvedor"
3. Clique em "Carregar sem compactação"
4. Selecione a pasta `focus-vault/`

## Características

- **Sem pausa/stop** — O foco vai até o final do timer
- **Persistência** — Fechar o Chrome e reabrir não interrompe o foco
- **Bloqueio real** — Usa `declarativeNetRequest` (nível de rede)
- **40 frases motivacionais** — Exibidas na página de bloqueio
- **Eventos** — Log local de ações (pronto para Supabase)

## Stack

- Chrome Extension Manifest V3
- Vanilla JS (ES Modules)
- CSS custom properties (tema escuro premium)
- `declarativeNetRequest` para bloqueio
- `chrome.storage.local` para persistência
- `chrome.alarms` para timer confiável

## Versão

**v1.1.0** — UI premium integrada, seletor de tempo com confirmação, botões de whitelist na página de bloqueio.
