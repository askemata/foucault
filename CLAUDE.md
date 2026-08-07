# Claude Instructions for Foucault Bibliography Project

## ⚠️ IMPORTANT: Project Status (as of 2026-08-06)
- **Site:** https://askemata.github.io/foucault/
- **10 obras primárias em /content**

### Como o site é publicado
GitHub Pages serve **diretamente o branch `main`, na raiz** (Settings → Pages
→ Source: "Deploy from a branch" → `main` / `(root)`).

Não há workflow de build. O site é Docsify puro: os `.md` são carregados pelo
navegador em tempo de execução. Todo push em `main` publica automaticamente,
em cerca de 1 minuto.

- `.nojekyll` (arquivo vazio, na raiz) impede o GitHub de processar o site com
  Jekyll. **Não apagar.**
- `README.md` é a home page do Docsify. **Não apagar nem renomear** — sem ele
  a página inicial fica em branco.
- `_config.yml` é resquício do Jekyll e está inerte.

### Histórico: por que os workflows foram removidos (2026-08-06)
Existiam dois workflows (`publish.yml` e `deploy.yml`) que empurravam o site
para um branch `gh-pages` via `peaceiris/actions-gh-pages`. Isso quebrou a
publicação por ~5 horas:
- `publish.yml` falhava sempre (`cp -r . build/` copiava o diretório dentro de
  si mesmo);
- `deploy.yml` falhava por falta de `permissions: contents: write`;
- depois de corrigido, `deploy.yml` passou a atualizar `gh-pages` com sucesso,
  mas pushes feitos com `GITHUB_TOKEN` não disparam o build do Pages — o
  conteúdo chegava ao branch e nunca era publicado.

O site ficou congelado no commit `ca87b19` enquanto 4 obras novas eram
adicionadas sem aparecer. Ambos os workflows foram apagados e o Pages voltou a
servir `main` diretamente. **Não reintroduzir workflow de deploy** — este site
não precisa de build.

## How to Continue
If context ends, load this file and the memory at:
`/home/marcio/.claude/projects/-home-marcio-Dropbox-DropsyncFiles-Blog-Foucault/memory/project_state.md`

Then follow the workflow below.

# Projeto: Michel Foucault's Bibliography

Site estático (Docsify) que documenta cronologicamente as obras de Michel
Foucault e a fortuna crítica sobre ele, de 1954 até hoje.

## Idioma
O site é inteiramente em português: resumos, descrições, glosas, textos de
interface e tags. Só o título do site permanece em inglês. Títulos de obras
ficam na língua original.

## Convenções de conteúdo
- Arquivos ficam em /content, nomeados como AAAA_autor_[titulo-curto].md
- Todo arquivo segue o template de frontmatter + corpo já estabelecido
  (title, author, type, date, url + referência ABNT + resumo de 4
  parágrafos + palavras-chave).
- type: "primary" = texto do próprio Foucault → adicionar #foucault-primaria
  type: "secondary" = texto sobre Foucault por outro autor → adicionar
  #foucault-secundaria
- Tags em português, sem acentos, separadas por hífen (#razao-desrazao,
  #cuidado-de-si). Reutilizar as existentes sempre que possível.
- Sempre incluir palavras-chave temáticas relevantes além das obrigatórias.

## Sempre linkar o que for citado
Toda obra, artigo, revista ou autor mencionado deve levar a algum lugar. Vale
para as fichas, para as páginas-índice e para o índice de palavras-chave.

**Se a obra citada já tem ficha no site**, o link é interno:
`[Histoire de la folie](/content/histoire_de_la_folie.md)`. Isso é o que
transforma a bibliografia numa rede em vez de uma lista.

**Se não tem ficha**, o link é externo, e vale esta ordem de preferência:

1. DOI (`https://doi.org/...`) — o mais estável que existe
2. Página da publicação original: editora, revista, coleção
3. Repositório institucional ou arquivo de acesso aberto
4. WorldCat, como último recurso de identificação

Prefira sempre a **página de base da obra** (a landing page da editora, o
registro do periódico) ao link direto de um PDF: PDFs mudam de endereço e sites
os movem de lugar, enquanto o registro tende a permanecer.

O campo `url:` do frontmatter segue a mesma ordem — é ele que alimenta os
metadados de citação e a exportação para o Zotero.

**Nunca inventar URL.** Link não verificado é pior que link ausente, porque
parece confiável. Se não achou uma fonte que possa conferir, deixe sem link e
me avise — mesma regra dos dados bibliográficos que não se consegue confirmar.

## Navegação: a barra lateral não cresce
`_sidebar.md` tem cinco itens fixos e **não deve receber links de obras**. O
Docsify desdobra sozinho os subitens da página ativa, via `subMaxLevel: 2` no
index.html: os cabeçalhos `## AAAA` de primary.md/secondary.md viram os anos, e
os `## A`..`## Z` de keywords.md viram as letras. É o que mantém a navegação
utilizável quando a bibliografia chegar aos milhares de itens.

## Regra de ouro: aprovação antes de publicar
NUNCA faça `git commit` ou `git push` sem antes:
1. Mostrar a lista dos arquivos criados/alterados nesta rodada;
2. Aguardar minha confirmação explícita (ex: "pode subir", "aprovado");
Somente após a confirmação, faça commit e push.

## Manutenção automática a cada lote de conteúdo novo
Sempre que novos arquivos forem criados em /content, atualizar também:
- primary.md ou secondary.md (item sob o cabeçalho `## AAAA` do ano; criar o
  cabeçalho na posição cronológica correta se o ano ainda não existir)
- keywords.md (adicionar/atualizar entradas das #keywords novas)

Não tocar em _sidebar.md — ver a seção "Navegação" acima.

O comando `/foucault-lote [n]` executa esse fluxo inteiro, com a trava de
aprovação embutida. Está versionado em `.claude/commands/foucault-lote.md`.
