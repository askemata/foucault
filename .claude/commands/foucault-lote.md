---
description: Pesquisa e gera um lote de novas fichas bibliográficas de Foucault, em ordem cronológica, a partir de onde /content parou
argument-hint: "[quantidade de textos, padrão 3, máximo 5]"
---

Gere até **$1** novos arquivos markdown sobre Michel Foucault (se nenhum número
foi informado, use 3; nunca ultrapasse 5), seguindo a ordem cronológica de 1954
até hoje, a partir de onde a bibliografia já publicada em `/content` parou.

**O site é inteiramente em português.** Resumos, descrições, glosas e tags são
em português; só o título do site permanece em inglês. Títulos de obras ficam na
língua original.

## 1. Levantar o que já existe

Leia `/content`, `primary.md`, `secondary.md` e `keywords.md` antes de qualquer
coisa. Monte a lista do que já está coberto e identifique, cronologicamente, os
próximos textos ainda ausentes.

Estado conhecido do acervo (confira, pode ter mudado):

- As **10 obras primárias publicadas em vida** por Foucault (1954–1984) já estão
  cobertas. A continuação natural são as obras póstumas (cursos do Collège de
  France, *Dits et Écrits*, *Les Aveux de la chair*) e a **fortuna crítica**, que
  começou em 1961 e está coberta até 1963.
- Se for começar uma categoria nova, diga isso explicitamente antes de gerar,
  para eu poder redirecionar.

## 2. Pesquisar

Faça pesquisa real sobre cada texto antes de escrever — não escreva de memória.
Confirme editora, ano, paginação e tradução. Cada ficha precisa de uma URL
verificável (WorldCat, editora, DOI ou repositório institucional). Se não
conseguir confirmar um dado, **deixe-o de fora e me diga qual é a incerteza**,
em vez de preencher por suposição.

## 3. Criar os arquivos

Um `.md` por texto em `/content`, nomeado `AAAA_autor_titulo-curto.md`
(minúsculas, sem acentos, palavras separadas por `_`).

Template obrigatório — siga exatamente, é o que o `index.html` sabe interpretar:

```markdown
---
title: "Título da obra"
author: "Nome do Autor"
type: primary | secondary
date: "AAAA"
url: "https://..."
---

# Título da obra

**Referência ABNT completa:**
SOBRENOME, Nome. *Título*. Cidade: Editora, ano. 000 p.

**Tradução para o inglês:**
[somente se aplicável]

## Resumo

[4 parágrafos, 3 a 5 frases cada, em português]

**Palavras-chave:** #tema1 #tema2 ... #foucault-primaria
```

Regras:

- `type: primary` → texto do próprio Foucault → tag `#foucault-primaria`
- `type: secondary` → texto sobre Foucault → tag `#foucault-secundaria`
- As aspas em `title`, `author`, `date` e `url` são obrigatórias.
- **Tags em português, sem acentos, separadas por hífen** (`#razao-desrazao`,
  `#cuidado-de-si`, `#saber-poder`). Reutilize as existentes sempre que puder —
  levante-as com `grep -h '^\*\*Palavras-chave' content/*.md`.
- Nenhuma tag repetida dentro da mesma ficha.

## 4. Atualizar os índices

**A barra lateral não se toca.** O `_sidebar.md` tem cinco itens fixos e se
desdobra sozinho a partir dos cabeçalhos `## AAAA` das páginas-índice — é o que
mantém a navegação utilizável quando a bibliografia crescer.

**`primary.md` ou `secondary.md`** — acrescente a obra sob o cabeçalho `## AAAA`
do seu ano. Se o ano ainda não existe, crie o cabeçalho na posição cronológica
correta. Formato do item:
`- [Título](/content/arquivo.md) — glosa de meia linha`
Em `secondary.md`, prefixe o título com o sobrenome do autor:
`- [Roland Barthes: De part et d'autre](...)`

**`keywords.md`** — para cada tag temática usada:

- Se a seção já existe, acrescente a obra como item:
  `- [AAAA - Título curto](/content/arquivo.md) — glosa de meia linha`
- Se não existe, crie `### Nome do Tema` sob a letra correta, com uma linha de
  descrição antes dos itens, seguindo o formato das seções vizinhas.
- Mantenha a ordem alfabética das seções dentro de cada letra, e das letras
  entre si. Se precisar de uma letra nova, crie o cabeçalho `## X`.
- O índice é **curado**: nem toda tag vira seção. Agrupe temas próximos em vez
  de criar uma seção por tag.

## 5. Parar e me mostrar

**Não faça commit nem push ainda.** Me apresente:

- a lista dos arquivos criados, com um resumo de uma linha cada;
- as seções novas ou alteradas em `keywords.md` e na página-índice;
- qualquer dado bibliográfico que você não conseguiu confirmar.

Aguarde minha aprovação explícita ("pode subir", "aprovado").

## 6. Verificar antes de me mostrar

Rode estas checagens e me relate o resultado:

```bash
# nenhum link apontando para arquivo inexistente
grep -ohP '\]\(\K/[^)]+' keywords.md primary.md secondary.md _sidebar.md | sort -u \
  | while read l; do [ -e "${l#/}" ] || echo "QUEBRADO: $l"; done

# o frontmatter de toda ficha continua legível pelo parser do site
grep -L '^title: "' content/*.md
```

## 7. Publicar, após a aprovação

1. `git add` dos arquivos específicos e `git commit`.
2. Tente `git push origin main`. **Este ambiente normalmente não tem credenciais
   do GitHub** — se falhar com `could not read Username`, não insista e não peça
   meu token: me mostre o comando para eu rodar no meu terminal.
3. O GitHub Pages serve `main` na raiz e publica sozinho em ~1 minuto. Não existe
   workflow de deploy e **não se deve criar um** — veja o `CLAUDE.md`.
4. Verifique contra o **site ao vivo**, nunca contra o branch:

```bash
curl -sI https://askemata.github.io/foucault/ | grep -i last-modified
curl -so /dev/null -w '%{http_code}\n' https://askemata.github.io/foucault/content/ARQUIVO_NOVO.md
```

## 8. Se acabou

Se todos os textos daquela categoria já estiverem cobertos até a data atual, não
force conteúdo novo: confirme a conclusão, informe a data final coberta e sugira
qual categoria faz sentido atacar em seguida.
