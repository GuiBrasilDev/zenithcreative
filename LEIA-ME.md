# Zenith Creative — site

Site de duas páginas, sem build e sem dependência: é só HTML, CSS e JavaScript puro.
Cada página é um arquivo único (o CSS e o JS estão dentro dela).

```
zenith-site/
├── index.html        página principal (hero, trabalhos, serviços, processo, contato)
├── portfolio.html    galeria com filtro e visualização ampliada
└── assets/           logos, artes e vídeos
```

## Publicar no GitHub Pages

1. Crie o repositório e suba a pasta inteira (`index.html` precisa ficar na raiz).
2. Settings → Pages → Source: `Deploy from a branch` → branch `main`, pasta `/ (root)`.
3. O site sai em `https://usuario.github.io/repositorio/`.

Funciona igual em Netlify ou Vercel: é só arrastar a pasta.

## Adicionar uma arte nova no portfólio

Coloque o arquivo em `assets/` e adicione um bloco na lista `TRABALHOS`, lá no
`<script>` do final do `portfolio.html`:

```js
{
  nome: "Nome da peça",
  cliente: "Cliente ou tipo de post",
  tipo: "esportivo",          // "esportivo" ou "corporativo"
  video: false,               // true se for .mp4
  arquivo: "assets/arquivo.png"
  // se video: true, adicione também  capa: "assets/capa.jpg"
}
```

Os filtros (Todos / Esportivo / Corporativo / Motion) se atualizam sozinhos —
"Motion" pega tudo que tem `video: true`.

Para vídeo, gere a capa do primeiro frame (fica como imagem enquanto carrega):

```bash
ffmpeg -i assets/arquivo.mp4 -vframes 1 assets/capa-arquivo.jpg
```

Formato ideal das artes: **1080×1350** (4:5). Os cards são recortados nessa
proporção, então arte quadrada ou story também entram, mas cortam nas bordas.

Os três destaques da home ficam direto no HTML do `index.html`, dentro de
`<section id="trabalhos">` — troque quando quiser rodar a vitrine.

## Onde trocar os dados de contato

O número do WhatsApp (`5519982375594`) e o Instagram aparecem em alguns pontos.
Busque por `wa.me` e por `instagram.com` nos dois arquivos e troque tudo de uma vez.
A mensagem que já vai preenchida no WhatsApp é o trecho depois de `?text=`.

## Decisões de design

- **Paleta 100% monocromática.** Nenhum elemento da interface tem cor: fundo
  asfalto (`#0B0B0C`), traço off-white do logo (`#E8E5E0`) e cinzas. A única cor
  da página vem das artes. Se um dia entrar uma cor de destaque na interface, ela
  compete com o trabalho exposto.
- **Tipografia:** Anton nos títulos (a mesma pegada condensada e pesada dos
  cartazes esportivos) e Archivo no texto e nos rótulos. Vêm do Google Fonts;
  sem internet, o navegador cai numa fonte parecida sem quebrar o layout.
- **Revelação em spray:** cada bloco entra com um corte de cima pra baixo, feito
  o traço de uma lata. É o único movimento da página, e ele respeita
  `prefers-reduced-motion`.
- **Numeração 01/02/03** só aparece em "Como funciona", porque ali a ordem
  significa alguma coisa de verdade.
