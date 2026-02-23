# CHANGELOG — Focus Vault

## v1.2.0 — Bloqueio robusto + Enforcement de abas

### 🔒 Fix: Sites não bloqueados (x.com, xbox.com, etc.)
**Causa raiz**: A regra DNR `|http` era uma única regra catch-all que em certas situações do Chrome (prerender, speculative loading, autocomplete com preconnect) não interceptava a navegação.

**Solução**: 
- DNR agora usa **duas regras de bloqueio separadas** — uma para `|http://` e outra para `|https://` — mais explícitas e confiáveis
- Regras de allow agora incluem variante `www.` automaticamente
- `isAllowed()` reescrito com `safeParse()` que lida com URLs com ou sem protocolo
- Comparação de domínios agora é case-insensitive (`.toLowerCase()`)

### 🔄 Novo: Enforcement de abas já abertas
**3 camadas de proteção além do DNR:**

1. **`tabs.onActivated`** — Quando o usuário troca para uma aba, verifica se a URL é permitida. Se não for, redireciona imediatamente para `blocked.html`
2. **`tabs.onUpdated`** — Quando a URL de uma aba muda (back/forward, SPA navigation, etc.), verifica e bloqueia se necessário
3. **`webNavigation.onCommitted`** — Backup para navegações que passam pelo DNR (bfcache, prerender activation)

**Ao iniciar o foco**: `enforceAllTabs()` escaneia TODAS as abas abertas e redireciona as que não estão na whitelist.

**Ao restaurar estado** (Chrome reiniciado): Também escaneia todas as abas.

### 🖼️ Novo favicon
- Ícones regenerados a partir da nova imagem (sem fundo)
- 16×16, 48×48, 128×128 + favicon.ico

### 🛡️ DNR: Regras de allow melhoradas  
- `chrome://` e `chrome-extension://` sempre permitidos (priority 100)
- Variantes www. geradas automaticamente para itens de domínio
- Extension ID explícito na regra de allow (mais seguro)

### 🐛 Fix: RESET_SESSION agora limpa regras DNR
- Antes, ao resetar a sessão pela Options/Dev Mode, as regras DNR podiam ficar ativas
- Agora `RESET_SESSION` chama `updateDNRRules([], false)` explicitamente

---

## v1.1.0 — UI Premium integrada

- Tema escuro (#121214, #E8530E, JetBrains Mono)  
- Seletor de tempo custom com popover (✅ confirma, ✕ cancela)
- Botões de whitelist na blocked.html (até 5, redirect direto)
- Logo + favicon inseridos
- Onboarding refinado com animações
