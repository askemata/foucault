# Claude Instructions for Foucault Bibliography Project

## ⚠️ IMPORTANT: Project Status (as of 2026-08-06)
- **Status:** ✅ FUNCTIONAL at commit 4849b45
- **Site:** https://askemata.github.io/foucault/
- **6 works published and working**
- **DO NOT change GitHub Pages configuration**

## How to Continue
If context ends, load this file and the memory at:
`/home/marcio/.claude/projects/-home-marcio-Dropbox-DropsyncFiles-Blog-Foucault/memory/project_state.md`

Then follow the workflow below.

# Projeto: Michel Foucault's Bibliography

Site estático (Docsify) que documenta cronologicamente as obras de Michel
Foucault e a fortuna crítica sobre ele, de 1954 até hoje.

## Convenções de conteúdo
- Arquivos ficam em /content, nomeados como AAAA_autor_[titulo-curto].md
- Todo arquivo segue o template de frontmatter + corpo já estabelecido
  (title, author, type, date, url + referência ABNT + resumo de 4
  parágrafos + palavras-chave).
- type: "primary" = texto do próprio Foucault → adicionar #foucault-primaria
  type: "secondary" = texto sobre Foucault por outro autor → adicionar
  #foucault-secundaria
- Sempre incluir palavras-chave temáticas relevantes além das obrigatórias.

## Regra de ouro: aprovação antes de publicar
NUNCA faça `git commit` ou `git push` sem antes:
1. Mostrar a lista dos arquivos criados/alterados nesta rodada;
2. Aguardar minha confirmação explícita (ex: "pode subir", "aprovado");
Somente após a confirmação, faça commit e push.

## Manutenção automática a cada lote de conteúdo novo
Sempre que novos arquivos forem criados em /content, atualizar também:
- _sidebar.md (adicionar os novos links, em ordem cronológica)
- keywords.md (adicionar/atualizar entradas das #keywords novas)
