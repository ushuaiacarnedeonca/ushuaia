# Site — Carne de Onça Ushuaia

Site do **Ushuaia** (Curitiba): página principal de pedidos mais três artigos de blog.
Tudo estático — HTML, CSS e um bloco pequeno de JavaScript. **Não tem build, não tem
dependência, não precisa de Node.** É publicar a pasta como está.

```
index.html          página principal
blog/               três artigos
assets/             fotos, logos e selos
netlify.toml        configuração (só vale na Netlify)
_headers            cabeçalhos HTTP (só vale na Netlify)
```

Produzido pela Nexum360 no âmbito da consultoria SEBRAE-PR.

---

## O que falta antes de publicar

### 1. Tirar o bloqueio de indexação

O arquivo **`_headers`** contém hoje:

```
X-Robots-Tag: noindex, nofollow
```

Isso **impede o Google de indexar o site**, e foi assim de propósito enquanto a página
esteve em prévia.

Quando o site entrar no ar valendo, **apague essa linha**. Se esquecer, o site funciona
para quem tem o link e nunca aparece na busca — o que, para um delivery, corta a maior
fonte de cliente novo.

### 2. Trocar o endereço do site nas 5 tags de compartilhamento

O site esteve publicado em `https://mktcastro-bit.github.io/ushuaia/`, e esse endereço
ficou gravado nas tags que o WhatsApp, o Instagram e o Facebook leem para montar a prévia
do link. São **cinco lugares**:

| Arquivo | Linha | Tag |
|---|---|---|
| `index.html` | 14 | `og:image` |
| `index.html` | 15 | `og:url` |
| `blog/o-que-e-carne-de-onca.html` | 14 | `og:image` |
| `blog/indicacao-de-procedencia.html` | 14 | `og:image` |
| `blog/vegana-e-sem-gluten.html` | 14 | `og:image` |

Troque `https://mktcastro-bit.github.io/ushuaia/` pelo **domínio final**. Se não trocar,
quem compartilhar o link no WhatsApp verá a prévia apontando para o endereço antigo.

Com um editor de texto, é substituir tudo de uma vez. No terminal, dentro da pasta:

```bash
grep -rl "mktcastro-bit.github.io/ushuaia" . \
  | xargs sed -i '' 's|https://mktcastro-bit.github.io/ushuaia|https://SEU-DOMINIO.com.br|g'
```

### 3. Ligar os dois links do rodapé

No bloco **"Onde nos achar"** do rodapé, os dois links ainda não têm destino:

```html
<a href="#">Instagram</a>
<a href="#">Google Meu Negócio</a>
```

Troque o `#` pelos endereços reais. O do Google Meu Negócio se obtém buscando o
estabelecimento no Google Maps e usando **Compartilhar → Copiar link**.

Se não houver um dos dois, é melhor **apagar a linha** do que deixar apontando para `#` —
um link que não faz nada passa impressão de página abandonada.

> O endereço físico foi removido do rodapé por não estar disponível. Para devolver, basta
> uma linha no mesmo bloco de Contato:
> `<a href="LINK-DO-MAPA">Rua, número — bairro</a>`

---

## Como publicar

A pasta é a raiz do site. `index.html` é a página inicial.

### Netlify (o `netlify.toml` já está pronto)

1. Suba esta pasta para um repositório no GitHub
2. No Netlify: **Add new site → Import an existing project → GitHub**
3. Escolha o repositório. **Build command:** vazio. **Publish directory:** `.`
4. Deploy

### Vercel

**Add New → Project**, importe o repositório.
**Framework Preset:** Other · **Build Command:** vazio · **Output Directory:** `.`

### Hospedagem comum (cPanel, FTP, Apache, nginx)

Copie o conteúdo da pasta para a raiz pública (`public_html`, `www` ou similar).
Nesse caso `netlify.toml` e `_headers` são **ignorados** — as regras deles precisariam ir
para o `.htaccess` ou para a configuração do servidor.

---

## O que mexer depois

### Número do WhatsApp

Todos os botões de pedido usam o mesmo número, definido **uma vez só** no fim do
`index.html`:

```js
const WHATSAPP = '5541999119195';   // (41) 99911-9195
```

Formato: país + DDD + número, **só dígitos**. Trocar ali muda todos os botões.
Logo abaixo estão as mensagens que já vão escritas na conversa.

### Textos e fotos

Todo o texto está direto no HTML. As imagens ficam em `assets/`, com nomes que indicam o
uso (`foto-hero-1600.jpg` é a foto grande do topo, com a versão `900` para telas menores;
`cur-*.jpg` são as fotos de Curitiba; `selo-*.png` são os selos).

Ao trocar uma foto, **mantenha o mesmo nome de arquivo** — assim não é preciso mexer no HTML.

---

## Detalhes técnicos

- **Fontes** vêm do Google Fonts e do Fontshare, por CDN — exigem internet.
- **Sem analytics, sem formulário, sem cookies.** O único destino externo é o WhatsApp.
- **Links do blog são relativos**, então funcionam em qualquer domínio ou subpasta.
- **Imagens somam cerca de 2 MB.** Funciona, mas se puder converter para WebP, o ganho em
  celular é grande — os maiores são as fotos do topo e as de Curitiba.
- O `netlify.toml` guarda cache longo para `assets/*`. Se trocar uma imagem mantendo o
  nome, quem já visitou pode continuar vendo a antiga por um tempo — para forçar, mude o
  nome do arquivo e ajuste o HTML.

---

## Contato

Dúvidas sobre conteúdo, texto ou estratégia da página:
**Luciano Castro — Nexum360**.
