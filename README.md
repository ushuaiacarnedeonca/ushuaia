# Site — Carne de Onça Ushuaia

Site institucional e de pedidos do **Ushuaia** (Curitiba). Página única, estática:
HTML, CSS e um bloco pequeno de JavaScript. **Não tem build, não tem dependência,
não precisa de Node.** É publicar a pasta como está.

Produzido pela Nexum360 no âmbito da consultoria SEBRAE-PR.

---

## ⚠️ Antes de publicar — leia este item

O arquivo **`_headers`** contém hoje:

```
X-Robots-Tag: noindex, nofollow
```

Isso **impede o Google de indexar o site**. Foi assim de propósito enquanto a página
esteve em prévia, para não aparecer em busca antes da hora.

**Quando o site entrar no ar de verdade, apague essas duas palavras** — deixe a linha
`X-Robots-Tag` de fora, ou remova o arquivo inteiro se a hospedagem não usar `_headers`.
Se esquecer, o site funciona normalmente para quem tem o link, mas **nunca aparece no
Google** — o que, para um delivery, elimina a maior fonte de clientes novos.

---

## Como publicar

A pasta é a raiz do site. `index.html` é a página inicial.

### Netlify (o `netlify.toml` já está pronto)

1. Suba esta pasta para um repositório no GitHub
2. No Netlify: **Add new site → Import an existing project → GitHub**
3. Escolha o repositório. **Build command:** deixe vazio. **Publish directory:** `.`
4. Deploy

### Vercel

1. **Add New → Project**, importe o repositório
2. **Framework Preset:** Other · **Build Command:** vazio · **Output Directory:** `.`

### Hospedagem comum (cPanel, FTP, Apache, nginx)

Copie todo o conteúdo da pasta para a raiz pública (`public_html`, `www` ou similar).
Nesse caso o `netlify.toml` é ignorado, e o `_headers` **também** — as regras dele
precisariam ir para o `.htaccess` ou para a configuração do servidor.

---

## O que mexer depois

### Número do WhatsApp

Todos os botões de pedido apontam para o mesmo número, definido **uma vez só** no fim do
`index.html`:

```js
const WHATSAPP = '5541999119195';   // (41) 99911-9195
```

Formato: código do país + DDD + número, **só dígitos**. Trocar ali muda todos os botões.

Logo abaixo estão as mensagens que já vão escritas na conversa:

```js
const MSG = {
  pedido: 'Olá! Vim pelo site e quero fazer um pedido.',
  b2b:    'Olá! Sou de um hotel e queria falar sobre parceria.'
};
```

### Textos e fotos

Todo o texto está direto no `index.html`. As imagens ficam em `assets/`, e os nomes
indicam o uso (`foto-hero-1600.jpg` é a foto grande do topo, com a versão `900` para
telas menores).

Ao trocar uma foto, **mantenha o mesmo nome de arquivo** — assim não é preciso mexer no
HTML.

---

## Detalhes técnicos

- **Fontes** vêm do Google Fonts e do Fontshare, por CDN. Exigem internet e não podem
  ser bloqueadas por firewall.
- **Sem analytics, sem formulário, sem cookies.** O único destino externo é o WhatsApp.
- **Imagens somam cerca de 1,2 MB.** Funciona, mas se a hospedagem permitir, vale
  converter para WebP e reduzir — o ganho maior está em `foto-hero-1600.jpg` (292 KB),
  `foto-tradicional-1x1.jpg` (281 KB) e nos dois logos em PNG, que passariam bem para
  SVG ou WebP.
- O `netlify.toml` guarda cache longo para `assets/*`. Se trocar uma imagem mantendo o
  nome, o navegador de quem já visitou pode continuar mostrando a antiga por um tempo —
  para forçar, mude o nome do arquivo e ajuste o HTML.

---

## Contato

Dúvidas sobre o conteúdo, o texto ou a estratégia da página:
**Luciano Castro — Nexum360**.
