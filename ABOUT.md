# Sobre o projeto

## Visão geral

*Michel Foucault's Bibliography* é uma coleção digital de acesso aberto reunindo as obras de Michel Foucault e a fortuna crítica sobre seu pensamento. O projeto busca apoiar a pesquisa e o ensino oferecendo:

- Informação bibliográfica completa, com referência em ABNT e tradução para o inglês quando existe
- Resumos e indexação temática para orientação rápida
- Exportação direta para gerenciadores de referências (Zotero, Mendeley e outros)
- Busca em texto integral sobre todos os resumos e metadados

## Por que este projeto

A obra de Foucault atravessa cinco décadas e várias línguas, e muda de forma significativa ao longo do percurso — dos primeiros trabalhos sobre loucura e medicina à arqueologia e à genealogia, e daí à ética e à governamentalidade dos últimos anos. Uma bibliografia organizada cronologicamente torna esse movimento visível, o que uma lista alfabética não faria.

A fortuna crítica recebe o mesmo tratamento cronológico, e por um motivo parecido: as respostas a Foucault formam elas próprias uma história, em que cada leitura responde às anteriores.

O projeto procura ser acessível sem abrir mão do rigor: cada entrada oferece contexto suficiente para quem chega agora, e dados precisos o bastante para quem já trabalha com o material.

## Arquitetura técnica

- **Renderização:** [Docsify](https://docsify.js.org) — lê os arquivos Markdown no navegador, em tempo real
- **Sem etapa de compilação** — não há gerador de site nem workflow de deploy; os arquivos servidos são os arquivos do repositório
- **Hospedagem:** [GitHub Pages](https://pages.github.com), servindo o branch `main` na raiz. Todo envio ao repositório publica em cerca de um minuto
- **Exportação:** metadados Highwire Press no `<head>` de cada ficha, e arquivos `.ris` gerados no navegador
- **Tema:** CSS responsivo, com modo claro e escuro

## Como as fichas são organizadas

Os arquivos ficam em `/content`, nomeados `AAAA_autor_titulo-curto.md`, e seguem este formato:

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
[referência]

**Tradução para o inglês:**
[quando aplicável]

## Resumo

[quatro parágrafos]

**Palavras-chave:** #tema1 #tema2 ... #foucault-primaria
```

`type: primary` marca textos do próprio Foucault, com a tag `#foucault-primaria`. `type: secondary` marca textos sobre ele, com `#foucault-secundaria`.

Ao acrescentar uma ficha, é preciso atualizar também a página-índice correspondente (`primary.md` ou `secondary.md`) e o [índice de palavras-chave](/keywords.md). A barra lateral não precisa ser tocada: ela se desdobra sozinha a partir dos cabeçalhos de ano dessas páginas.

## Metadados de citação

Cada ficha expõe seus dados por dois caminhos:

**Metadados Highwire Press** — injetados no `<head>` quando a ficha é aberta, permitindo importação direta pelo botão do Zotero no navegador: `citation_title`, `citation_author`, `citation_publication_date`, `citation_public_url`.

**Botão de exportação** — gera um arquivo `.ris` compatível com Zotero, Mendeley, EndNote, BibDesk, Citavi e a maioria dos gerenciadores.

## Critérios de conteúdo

- **Obras primárias:** publicações, cursos e entrevistas do próprio Foucault
- **Fortuna crítica:** monografias, artigos, teses e coletâneas sobre sua obra
- **Resumos:** quatro parágrafos, claros e precisos, úteis tanto a quem chega agora quanto a especialistas
- **Palavras-chave:** reutilizar as existentes sempre que possível; criar novas com parcimônia
- **Exatidão:** conferir editora, ano, paginação e tradução antes de publicar. Dado que não se consegue confirmar não entra na referência — a incerteza é registrada em vez de preenchida por suposição

## Licença e atribuição

A definir pelo mantenedor do projeto.

## Créditos

Construído com [Docsify](https://docsify.js.org) e hospedado no [GitHub Pages](https://pages.github.com).

---

Dúvidas ou sugestões? Abra uma issue no repositório ou entre em contato com o mantenedor.
