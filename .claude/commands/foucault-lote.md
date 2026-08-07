---
description: Pesquisa e gera um lote de novas fichas bibliográficas de Foucault, em ordem cronológica, a partir de onde /content parou
argument-hint: "[quantidade de textos, padrão 3, máximo 5]"
---

Gere até **$1** novos arquivos markdown sobre Michel Foucault (se nenhum número
foi informado, use 3; nunca ultrapasse 5), seguindo a ordem cronológica de 1954
até hoje, a partir de onde a bibliografia já publicada em `/content` parou.

## 1. Levantar o que já existe

Leia `/content`, `_sidebar.md` e `keywords.md` antes de qualquer coisa. Monte a
lista do que já está coberto e identifique, cronologicamente, os próximos
textos ainda ausentes.

Estado conhecido do acervo (confira, pode ter mudado):

- As **10 obras primárias publicadas em vida** por Foucault (1954–1984) já
  estão cobertas. Isso significa que a continuação natural são as obras
  póstumas (cursos do Collège de France, *Dits et Écrits*, *Les Aveux de la
  chair*) e a **fortuna crítica secundária**, também em ordem cronológica a
  partir de 1954.
- Se você for começar uma categoria nova (póstumas ou secundária), diga isso
  explicitamente antes de gerar, para eu poder redirecionar se quiser outra
  coisa.

## 2. Pesquisar

Faça pesquisa real sobre cada texto antes de escrever — não escreva de memória.
Confirme editora, ano, paginação e tradução. Cada ficha precisa de uma URL
verificável (WorldCat, editora, DOI ou repositório institucional). Se não
conseguir confirmar um dado, diga qual é a incerteza em vez de inventar.

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

**English translation:**
[somente se aplicável]

## Resumo

[4 parágrafos, 3 a 5 frases cada, em português]

**Palavras-chave:** #tema1 #tema2 ... #foucault-primaria
```

Regras do frontmatter:

- `type: primary` → texto do próprio Foucault → tag `#foucault-primaria`
- `type: secondary` → texto sobre Foucault → tag `#foucault-secundaria`
- As aspas em `title`, `author`, `date` e `url` são obrigatórias.
- O resumo é em **português**; as tags temáticas são em **inglês**
  (`#discourse`, `#power`, `#biopolitics`…), acompanhando o padrão já existente.

## 4. Atualizar os índices

**`_sidebar.md`** — insira cada obra em ordem cronológica, no formato
`- [AAAA - Título](/content/arquivo.md)`, dentro da seção correta
(*Primary Works* ou *Secondary Literature*).

**`keywords.md`** — para cada palavra-chave temática usada:

- Se a seção já existe, acrescente a obra como bullet:
  `- [AAAA - Título](/content/arquivo.md) — glosa de meia linha`
- Se não existe, crie `### Nome da Keyword` sob a letra correta (A–Z), com uma
  linha de descrição antes dos bullets, seguindo o formato das seções vizinhas.
- Mantenha a ordem alfabética das seções.

## 5. Parar e me mostrar

**Não faça commit nem push ainda.** Me apresente:

- a lista dos arquivos criados, com um resumo de uma linha cada;
- as seções novas ou alteradas em `keywords.md` e `_sidebar.md`;
- qualquer dado bibliográfico que você não conseguiu confirmar.

Aguarde minha aprovação explícita ("pode subir", "aprovado").

## 6. Publicar, após a aprovação

1. `git add` dos arquivos específicos e `git commit`.
2. Tente `git push origin main`. **Este ambiente normalmente não tem credenciais
   do GitHub** — se o push falhar com `could not read Username`, não insista e
   não peça meu token: me mostre o comando para eu rodar no meu terminal.
3. O GitHub Pages serve `main` na raiz e publica sozinho em ~1 minuto. Não
   existe workflow de deploy e **não se deve criar um** — veja o `CLAUDE.md`.
4. Verifique contra o **site ao vivo**, nunca contra o branch:

```bash
curl -sI https://askemata.github.io/foucault/ | grep -i last-modified
curl -so /dev/null -w '%{http_code}\n' https://askemata.github.io/foucault/content/ARQUIVO_NOVO.md
```

Um `200` no arquivo novo confirma a publicação.

## 7. Se acabou

Se todos os textos daquela categoria já estiverem cobertos até a data atual,
não force conteúdo novo: confirme a conclusão, informe a data final coberta e
sugira qual categoria faz sentido atacar em seguida.
