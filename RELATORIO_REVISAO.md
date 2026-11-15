# Relatório de Revisão — Centro Comercial Bonfim Lacerda

Data: 2026-11-15 · Nenhum commit foi feito. Todas as alterações estão no working tree para sua revisão.

## 🔴 Bugs funcionais corrigidos (app.js)

1. **Filtro de categoria falhava com acento** — os botões `data-filter` ("saúde", "comércio", "cartório", "serviços públicos") não retornavam nenhum resultado, porque a comparação usava o valor com acento contra a categoria normalizada do card. Agora o `data-category` é normalizado na renderização e o `cat` também é normalizado antes de comparar.
2. **Home ignorava o limite de 4 lojas** — `data-home-services="4"` era lido, mas `setupDirectory()` chamava `renderServices()` sem limite logo depois, sobrescrevendo e mostrando os 8. Agora `setupDirectory()` só re-renderiza quando há busca/filtros na página (ou seja, não na home).
3. **Busca com acento** — a função `norm` era local; agora é global e reutilizada. Busca por "cartorio" acha "Cartório".

## 🟠 Problemas de marcação / validade corrigidos

4. **`&` solto em texto visível** — em todos os HTMLs, "Lojas & Serviços", "Bonfim & Lacerda", "Histórias & Notícias" etc. usavam `&` sem escapar. Convertidos para `&amp;` (apenas em texto; URLs e atributos preservados, ex.: `&output=embed` do mapa).
5. **`&` em strings JS** que vão para `innerHTML` (nomes de estabelecimentos) — escapados para `&amp;`.
6. **`<body >`** com espaço sobrando em 7 páginas — normalizado para `<body>`.
7. **CSS morto removido** — `.hero-media`, `.hero:before`, `.subbrand`, `.slogan` eram regras da versão antiga, sem uso no HTML da v3.
8. **`data-name`** no card (escrito, nunca lido) — removido.
9. **Página "não encontrado"** da loja (loja.html?servico=…) melhorada: agora explica o problema e aponta ao diretório; ganhou estilo `.not-found`.
10. **Botões de filtro** ganharam `aria-pressed` (acessibilidade).

## 🟡 Textos revisados (clareza / coerência)

11. `centro.html` — "Um só destino: soluções." → "Um só destino: o que você precisa."; "voltados para a região central" → "voltados para o centro da cidade".
12. `contato.html` — frase prolixa sobre canais institucionais simplificada: "fale com a gente pelo Instagram oficial".
13. `historia.html` — "Bomfim & Lacerda Advocacia" (errado) → "Bonfim & Lacerda Advocacia"; "sala 07" → "Sala 07"; "Um endereço passa a reunir" → "O endereço passa a reunir"; "ligação com Independência" → "ligação com a cidade".
14. `noticias.html` — "conteúdos ligados" → "histórias ligadas" (evita "conteúdos" genérico).
15. `README.md` — "rodapé" → "rodapé" já estava ok; removida a frase "comportamento idêntico ao servidor" (imprecisa), substituída por explicação sobre `file://`.

## 🔵 Acessibilidade / qualidade

16. `alt` das imagens melhorados (hero, collage, story-cards, centro.html) — textos descritivos em vez de genéricos.
17. `not-found` com CSS dedicado (antes usava `btn` solto).

## ⚠️ Ponto de atenção (não mexi)

- `historia.html` no disco (107 KB, foto dos fundadores em base64 inline) é diferente do que está no commit atual (5,9 KB, que usa `fundadores.webp` externo). Você confirmou que quer manter a versão do disco. Ao comitar, o repositório passará a armazenar os 107 KB.
- Duas imagens em `assets/images/` não são referenciadas em nenhuma página: `bradesco-post.webp` e `joatan.webp`. Mantive (pode ser material futuro). Diga se quer remover.

## ✅ Verificações feitas

- `node --check app.js` — sintaxe OK
- 9 HTMLs validados: tags balanceadas, 0 problemas
- Todas as imagens referenciadas existem
- CSS: 230 chaves abertas / 230 fechadas
- Base64 do historia.html preservada (hash idêntico)
- Testes de comportamento (mock DOM): home=4 cards; /lojas=8; filtros "saúde"/"comércio"/"serviços públicos"/"cartório" funcionam; filtro por URL `?categoria=advocacia` funciona; busca "cartorio" acha "Cartório"

## 📝 Arquivos alterados (12)

README.md · assets/css/style.css · assets/js/app.js · centro.html · contato.html · historia.html · index.html · loja.html · lojas.html · lojista.html · memorias.html · noticias.html
