# Caderno de fichamentos

Página única para ler, filtrar e editar fichamentos de leitura de uma tese de
doutorado sobre securitização, riscoficação e climatização da mudança climática.
Sem build, sem dependências, sem framework.

**Este repositório contém apenas o aplicativo.** Nenhum fichamento está aqui.
O conteúdo fica num Gist secreto cujo ID é digitado no navegador e guardado só no
`localStorage` — ver `.gitignore`.

## O que faz

- **Matriz** — os campos-eixo de todas as fichas lado a lado, recortada pelos filtros.
- **Fichas** — os fichamentos completos, com edição de todos os campos no lugar.
  O bloco D (crítica, uso na tese, diálogo, brecha) aparece destacado: é a voz de
  quem fichou, não a do autor fichado.
- **Análise** — recalculada a cada edição: agrupamento por eixo, co-citação a partir
  do campo `refs`, todos os pares classificados (tensão, padrão, convergência
  independente), cruzamentos em que a célula vazia é a lacuna do corpus, rede de
  `[[links]]` com fichas órfãs e lista de pendências.

A análise cruza o que foi classificado à mão. Ela não lê os artigos e não sabe se a
classificação está certa — vocabulário inconsistente produz falsas distinções.

## Configurar

1. Criar um **Gist secreto** com um arquivo `caderno.json` (pode começar com `{}`).
2. Criar um **fine-grained PAT** com uma única permissão de conta: *Gists: read and write*.
3. Abrir o site → **Config** → colar o ID do Gist e o token.
4. **Buscar** puxa do Gist; **Enviar** grava. Conflito é detectado por timestamp:
   se o Gist mudou desde a última vez que este navegador o viu, ele pergunta antes
   de sobrescrever.

O token mora em `caderno-sync`, separado dos dados em `caderno-fichas-v1`, para não
entrar no backup exportado nem subir para o Gist.

## Fichas novas

Três caminhos, todos convergindo no mesmo formato:

- **+ Ficha** cria o esqueleto de 22 campos, com o bloco D já marcado como pendente.
- **Config → Importar** aceita um `caderno.json` inteiro (substitui tudo) ou uma
  ficha avulsa em JSON (acrescenta ou atualiza pelo `id`). É por aqui que entram as
  pré-fichas geradas fora do navegador.
- O script local `Invoke-Caderno.ps1` converte uma pasta de arquivos `.md` em
  `caderno.json`, para carga inicial ou trabalho em lote.

Depois de publicar, **o Gist é a fonte da verdade**. Editar os `.md` locais e o site
ao mesmo tempo diverge sem aviso.

## Formato de uma ficha

```json
{
  "id": "autorAAAA",
  "meta": { "autor": "", "ano": "", "titulo": "", "processo": "climatizacao",
            "nivel": "organizacional", "criterio": "comportamental",
            "regiao": ["india"], "refs": ["buzan1998"], "tags": [] },
  "secoes": [ { "codigo": "A1", "titulo": "Referência completa", "corpo": "…" } ]
}
```

Campos multivalorados (`regiao`, `refs`, `tags`, `filiacao`) são listas. Uma seção
cujo corpo começa com `> A preencher` entra automaticamente na lista de pendências.
