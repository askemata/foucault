# Como atualizar o site manualmente

Roteiro completo para acrescentar uma obra à bibliografia, da criação do arquivo
até a publicação. Sete passos.

O site é Docsify: os arquivos `.md` são lidos pelo navegador em tempo real. Não
há compilação, não há workflow de deploy. O que está no branch `main` é o que
está no ar.

---

## Passo 1 — Criar a ficha em `/content`

**Nome do arquivo:** `AAAA_autor_titulo-curto.md` — só minúsculas, sem acentos,
palavras separadas por `_`.

Exemplos reais: `1963_derrida_cogito_et_histoire_de_la_folie.md`,
`1971_l_ordre_du_discours.md`.

**Conteúdo**, exatamente neste formato:

```markdown
---
title: "Título da obra"
author: "Nome do Autor"
type: secondary
date: "1966"
url: "https://..."
---

# Título da obra

**Referência ABNT completa:**
SOBRENOME, Nome. *Título*. Cidade: Editora, ano. 000 p.

**Tradução para o inglês:**
SURNAME, Name. *Title*. Translated by Fulano. City: Publisher, year.

## Resumo

Primeiro parágrafo.

Segundo parágrafo.

Terceiro parágrafo.

Quarto parágrafo.

**Palavras-chave:** #tema1 #tema2 #foucault-secundaria
```

### Onde é fácil escorregar

- **As aspas em `title`, `author`, `date` e `url` são obrigatórias.** O `type`
  vai sem aspas.
- **`date` é texto**, mesmo sendo número: `date: "1966"`.
- `type: primary` para texto do próprio Foucault, `type: secondary` para texto
  sobre ele. A tag correspondente — `#foucault-primaria` ou
  `#foucault-secundaria` — é obrigatória e precisa combinar com o `type`.
- **Tags em português, sem acentos, com hífen:** `#razao-desrazao`,
  `#cuidado-de-si`. Nunca repita a mesma tag na mesma ficha.
- **Tradução para o inglês** só entra se existir; se não houver, apague as duas
  linhas.
- O resumo tem **quatro parágrafos**, de três a cinco frases cada, em português.
  Títulos de obras ficam na língua original.

### Linkar o que for citado

Toda obra, artigo ou revista mencionada deve levar a algum lugar.

- **Já tem ficha no site?** Link interno:
  `[*Histoire de la folie*](/content/histoire_de_la_folie.md)`
- **Não tem?** Link externo, nesta ordem: DOI → página da editora ou da revista
  → repositório institucional → WorldCat.
- Prefira a **página de base** da obra ao link direto de um PDF: o PDF muda de
  endereço, o registro permanece.
- **Nunca invente URL.** Link não verificado é pior que link ausente, porque
  parece confiável. Sem fonte que dê para conferir, deixe sem link.

Para ver quais tags já existem antes de criar uma nova:

```bash
grep -h '^\*\*Palavras-chave' content/*.md | grep -oP '#[\w-]+' | sort -u
```

---

## Passo 2 — Acrescentar à página do ano

Abra **`primary.md`** (obras de Foucault) ou **`secondary.md`** (fortuna
crítica). Ache o cabeçalho `## AAAA` do ano da obra. Se o ano ainda não existe,
crie-o na posição cronológica certa.

```markdown
## 1966

- [Título da obra](/content/1966_autor_titulo.md) — glosa de meia linha
```

Em `secondary.md`, o título vem precedido do nome do autor:

```markdown
- [Roland Barthes: De part et d'autre](/content/1961_barthes_de_part_et_d_autre.md) — a primeira grande resenha
```

A glosa depois do travessão é o que aparece na listagem. Vale escrever com
cuidado: é o que orienta quem está varrendo a página.

---

## Passo 3 — Atualizar `keywords.md`

Para cada tag temática usada. As `#foucault-*` não entram aqui — têm seção
própria.

**Se a seção já existe**, acrescente a obra como item:

```markdown
### Linguagem
Sistemas de signos e produção de sentido como modos de saber e de poder.
- [1971 - L'Ordre du Discours](/content/1971_l_ordre_du_discours.md) — a linguagem regulada pelo poder
- [1966 - Título novo](/content/1966_autor_titulo.md) — glosa de meia linha
```

**Se não existe**, crie sob a letra certa, com uma linha de descrição antes dos
itens:

```markdown
### Nome do Tema
Uma linha explicando o que o tema abrange.
- [1966 - Título novo](/content/1966_autor_titulo.md) — glosa de meia linha
```

Três regras:

- Mantenha a **ordem alfabética** das seções dentro de cada letra. Se precisar
  de uma letra que ainda não existe, crie o cabeçalho `## X` no lugar certo.
- No rótulo do link use **`AAAA - Título curto`** e, na fortuna crítica,
  **`AAAA - Sobrenome: Título`**.
- O índice é **curado**: nem toda tag vira seção. Agrupe temas próximos em vez
  de criar uma seção por tag.

---

## Passo 4 — Não toque no `_sidebar.md`

Ele tem cinco itens fixos e **não recebe links de obras**.

Os anos e as letras aparecem sozinhos na barra lateral, gerados a partir dos
cabeçalhos `##` que você editou nos passos 2 e 3 — é o `subMaxLevel: 2`
configurado no `index.html`. É o que impede a barra de crescer sem limite quando
a bibliografia chegar aos milhares de itens.

---

## Passo 5 — Testar localmente antes de subir

```bash
python3 -m http.server 8000
```

Abra **http://localhost:8000** e confira:

- a ficha nova abre e o título aparece;
- ela está listada na página do ano, e o ano aparece na barra lateral;
- os links do `keywords.md` levam à ficha;
- o botão **Exportar para o Zotero** baixa um `.ris` com o título certo. Se vier
  vazio ou com `undefined`, o frontmatter tem problema de aspas.

Para parar o servidor: `Ctrl+C`.

Checagem automática de links quebrados:

```bash
grep -ohP '\]\(\K/[^)]+' keywords.md primary.md secondary.md content/*.md | sort -u | while read l; do [ -e "${l#/}" ] || echo "QUEBRADO: $l"; done; echo fim
```

Silêncio antes do `fim` significa que está tudo certo.

---

## Passo 6 — Commit e push

Veja o que mudou:

```bash
git status
```

Adicione e comite:

```bash
git add -A && git commit -m "Acrescenta ficha de Fulano (1966)"
```

Envie:

```bash
git push origin main
```

Se pedir credenciais: usuário `askemata`, e no campo de senha o **token de
acesso pessoal**, não a senha do GitHub. A tela não mostra nada enquanto você
cola o token — é normal.

---

## Passo 7 — Confirmar que publicou

O GitHub Pages serve o branch `main` na raiz. Em cerca de um minuto está no ar.

```bash
curl -sI https://askemata.github.io/foucault/ | grep -i last-modified
```

Se o horário avançou depois do push, publicou. Para conferir a ficha específica:

```bash
curl -so /dev/null -w '%{http_code}\n' https://askemata.github.io/foucault/content/SEU_ARQUIVO.md
```

`200` confirma. Depois abra o site e dê `Ctrl+Shift+R` — o cache do navegador
costuma segurar a versão antiga por alguns minutos.

> **Verifique sempre contra o site ao vivo, nunca contra o branch.** Conferir
> que um arquivo chegou ao repositório não prova que ele está sendo servido. Foi
> exatamente essa confusão que, em agosto de 2026, deixou o site congelado por
> cinco horas enquanto quatro obras novas pareciam ter sido publicadas.

---

## Resumo

Criar o `.md` em `/content` → acrescentar em `primary.md` ou `secondary.md` →
atualizar `keywords.md` → testar em `localhost:8000` → `add`, `commit`, `push` →
conferir o site.

Todos os comandos deste guia supõem que você está na pasta do projeto:

```bash
cd "/home/marcio/Dropbox/DropsyncFiles/Blog Foucault"
```
