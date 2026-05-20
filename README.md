# LP Solar Template — 1Nort Digital

Template de Landing Page de captação solar pra clientes da 1Nort. Estrutura validada na LP Romasol Engenharia (2026-05-06) e refinada com feedback real de cliente (2026-05-07).

**Stack:** HTML/CSS/JS estático single-file (~80KB), sem build, sem dependências.

**Hospedagem:** GitHub Pages (conta `1NortDigital`).

---

## Como usar

### Opção A — via skill `/criar-lp-solar` (recomendado)
No Claude Code, rode:
```
/criar-lp-solar https://site-do-cliente.com.br
```
A skill raspa o site do cliente, extrai paleta, logo, dados e cria a LP do zero. Recomendado pra clientes novos.

### Opção B — via "Use this template" no GitHub
1. Clique em **Use this template** no repo `1NortDigital/lp-solar-template`
2. Crie como `1NortDigital/<cliente>-lp` (público)
3. Clone localmente e siga **Substituições** abaixo

### Opção C — manual (clone direto)
```bash
git clone https://github.com/1NortDigital/lp-solar-template <cliente>-lp
cd <cliente>-lp
rm -rf .git && git init
```
Depois siga **Substituições** abaixo.

---

## Substituições

Todos os placeholders no `index.html` estão no formato `{{NOME}}`. Aplique find/replace em cima do arquivo.

### Identidade do cliente (10)

| Placeholder | Exemplo | Descrição |
|---|---|---|
| `{{CLIENT_NAME}}` | `Romasol Engenharia` | Nome completo / razão social |
| `{{CLIENT_SHORT_NAME}}` | `Romasol` | Nome curto pra usar em frases |
| `{{CLIENT_SLUG}}` | `romasol` | Slug minúsculo, sem espaço (logo, cookies, repo) |
| `{{CLIENT_DOMAIN}}` | `romasolengenharia.com.br` | Domínio sem `https://` |
| `{{CLIENT_CITY}}` | `Uberlândia` | Cidade primária |
| `{{CLIENT_STATE}}` | `MG` | UF (2 letras) |
| `{{CLIENT_STATE_FULL}}` | `Minas Gerais` | Estado por extenso |
| `{{CLIENT_REGION}}` | `Triângulo Mineiro` | Região / área de atuação |
| `{{CLIENT_GEO_REGION}}` | `BR-MG` | Código ISO da região (BR-XX) |
| `{{CLIENT_LAT}}` | `-18.9186` | Latitude (geo schema) |
| `{{CLIENT_LON}}` | `-48.2772` | Longitude |

### WhatsApp (3)

| Placeholder | Exemplo | Descrição |
|---|---|---|
| `{{WHATSAPP_FULL}}` | `553497783777` | Só dígitos, com 55 + DDD + número |
| `{{WHATSAPP_DDD}}` | `34` | DDD (2 dígitos), pra placeholder de form |
| `{{WHATSAPP_DISPLAY}}` | `(34) 9 9778-3777` | Formatado pra exibir |

### Redes sociais (3)

| Placeholder | Exemplo | Descrição |
|---|---|---|
| `{{INSTAGRAM_URL}}` | `https://www.instagram.com/cliente/` | URL completo (com https) |
| `{{FACEBOOK_URL}}` | `https://www.facebook.com/cliente` | URL completo |
| `{{LINKEDIN_URL}}` | `https://www.linkedin.com/company/cliente` | URL completo |

### Paleta de cores (10)

| Placeholder | Exemplo | Descrição |
|---|---|---|
| `{{PRIMARY_COLOR}}` | `#0825c7` | Primária — azul vibrante (CTAs secundários, headers) |
| `{{PRIMARY_DARK}}` | `#020854` | Variação escura — hover, footer |
| `{{PRIMARY_DEEP}}` | `#020854` | Hero deep, fundos escuros (pode ser igual a `PRIMARY_DARK`) |
| `{{PRIMARY_CARD}}` | `#0048fe` | Cards / destaques claros |
| `{{PRIMARY_RGB}}` | `8,37,199` | RGB da `PRIMARY_COLOR` (sem `rgba()`, só os 3 números separados por vírgula) |
| `{{ACCENT_COLOR}}` | `#E9CE10` | Acento solar — CTAs principais (geralmente amarelo) |
| `{{ACCENT_DARK}}` | `#C9B00A` | Acento escuro |
| `{{ACCENT_LIGHT}}` | `#FFE74A` | Acento claro |
| `{{ACCENT_RGB}}` | `233,206,16` | RGB do `ACCENT_COLOR` |

> **Dica de RGB:** se o HEX for `#RRGGBB`, converta cada par hex pra decimal. Ex: `#0825c7` → `R=08=8`, `G=25=37`, `B=c7=199` → `8,37,199`.

---

## Assets a substituir

Além dos placeholders no HTML, troque os arquivos físicos da pasta `assets/` e `img/`:

### `assets/`
- **`logo-{{CLIENT_SLUG}}.png`** — logo do cliente (PNG transparente, ~1600x1068, deixar respiro)
- **`favicon.png`** — favicon 32x32 (pode gerar a partir da logo)

### `img/`
- **`homem-preocupado-conta.jpg`** — foto de problema (homem olhando conta de luz). Pode reusar a do template ou gerar nova via IA.
- **`1.png`, `2.png`, `3.png`, `4.png`** — 4 fotos reais de projetos do cliente (recomendado 800x800 quadrado)

---

## Conteúdo a customizar (marcado com `<!-- TODO -->`)

O HTML tem alguns blocos com texto-exemplo que você precisa substituir manualmente — busque por `TODO` no arquivo:

1. **Reviews (4 cards)** — substituir Cliente A/B/C/D por reviews reais com nome + cidade.
2. **Calculadora — select de cidades** — adicionar as cidades reais que o cliente atende.
3. **Form principal — select de cidades** — idem.
4. **Tags de cidades (seção "Cidades")** — substituir Cidade 2/3/4/5 pelas reais (12-18 ideal).
5. **Footer — unidades** — se o cliente tem mais de 1 unidade, descomentar o bloco e duplicar.

---

## Ativação técnica

### Webhook (n8n / Zapier / Make)
Edite a constante no `<script>` final do `index.html`:
```js
const WEBHOOK = 'https://seu-webhook.aqui';
```
Enquanto vazia, os formulários enviam apenas pelo WhatsApp e disparam evento dataLayer (GTM).

### Google Tag Manager
1. Substitua `GTM-XXXXXXXX` no bloco comentado do `<head>` pelo ID real do cliente
2. Descomente o bloco `<script>` do GTM e o `<noscript>` correspondente (se existir)

### Página de obrigado (opcional)
```js
const REDIRECT_OBRIGADO = 'https://seudominio.com.br/obrigado';
```

---

## Deploy no GitHub Pages

1. Crie/use o repo `1NortDigital/<cliente>-lp` (público)
2. Push do código
3. Settings → Pages → Source = `main`, folder = `/` (root)
4. URL viva: `https://1nortdigital.github.io/<cliente>-lp/`

### Domínio próprio (opcional)
1. Crie arquivo `CNAME` na raiz do repo com o domínio (ex: `lp.cliente.com.br`)
2. No DNS do cliente, aponte CNAME pra `1nortdigital.github.io`
3. Settings → Pages → Custom domain → confirmar
4. Ativar **Enforce HTTPS**

---

## Estrutura da página (14 seções)

```
topbar → header (sticky) → breadcrumb → hero → trust bar →
problema → como funciona → segmentos →
calculadora → diferenciais →
projetos (carrossel) → depoimentos →
form principal → FAQ → cidades → footer
```

Modais e overlays:
- Modal pós-calculadora (nome + tel)
- Painel WhatsApp flutuante (nome + tel + email + mensagem)

---

## Conversão

- **3 formulários:** lead principal (5 campos), modal pós-calc (nome+tel), painel WhatsApp (nome+tel+email+mensagem)
- **Fallback:** todos abrem WhatsApp se webhook não estiver configurado
- **Calculadora:** simulação de economia (95% da conta) + payback fixo "Até 5 anos"
- **UTM tracking:** captura `utm_source/medium/campaign/content/term`, `gclid`, `fbclid` da URL e cookie de 30d
- **GTM ready:** dataLayer disparando `lead_gerado` em todos os forms

---

## Padrões validados (não negociar)

- Naming repo: `<cliente>-lp` (igual `romasol-lp`, `naor-bueno-lp`, `viana-mota-lp`)
- Conta GitHub: `1NortDigital`
- Stack: single HTML/CSS/JS, sem build
- Estrutura: 14 seções fixas (ordem acima)
- Form principal: 5 campos (nome, WhatsApp, cidade, conta, segmento — sem email)
- Modal pós-calc: 2 campos (nome + tel)
- Segmentos: Residencial, Comercial, Empresarial, Fazenda/Rural

---

## Histórico

- **2026-05-06** — Criação da LP Romasol (referência viva)
- **2026-05-07** — Refresh com feedback real do cliente: nova paleta azul, payback "até 5 anos", 95% de economia, FAQ reescrita, footer com 2 unidades
- **2026-05-07** — Template extraído pra repo `lp-solar-template`
