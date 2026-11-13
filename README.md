# Fuzzy Catalog

Banco de dados de jogos e ports da comunidade usado pelo app **Fuzzy** (loja de jogos).
Por enquanto é só um catálogo: o app lê o `catalog.json` deste repositório e mostra a loja.

- **URL do catálogo:** `https://raw.githubusercontent.com/deivid22srk/fuzzy-catalog/main/catalog.json`
- **Schema:** versão 1 (veja abaixo).

## Aviso legal

- Este repositório **não hospeda jogos nem dados protegidos**. Cada entrada aponta para o
  release oficial do próprio projeto.
- Só entram ports e jogos de **código aberto** ou **freeware**.
- Ports que precisam dos arquivos do jogo original são marcados em `requirements`; você
  precisa ter uma cópia legal do jogo.

## Como o app usa

1. Baixa o `catalog.json` (com cache local e um `catalog.json` embutido no APK como reserva).
2. Mostra destaque, categorias e grade.
3. No detalhe, baixa o APK e abre o instalador do Android.

## Schema (v1)

```jsonc
{
  "schema": 1,
  "updated": "AAAA-MM-DD",
  "categories": [{ "id": "foss", "name": "Jogos livres" }],
  "games": [
    {
      "id": "openrct2",              // único
      "name": "OpenRCT2",
      "tagline": "Frase curta",
      "description": "Parágrafo",
      "developer": "OpenRCT2 Team",
      "license": "GPL-3.0",
      "licenseUrl": "https://...",
      "categories": ["ports", "engines"],
      "tags": ["Simulação", "Estratégia"],
      "requirements": "Requer os dados originais de ...", // ou null
      "sourceUrl": "https://github.com/...",
      "homepageUrl": "https://...",
      "featured": true,
      "accent": "#E4572E",          // cor da capa procedural
      "packageName": "io.openrct2", // para detectar se está instalado
      "type": "apk",                // "apk" ou "internal"
      "minAndroid": "7.0",
      "version": "0.5.7",
      "sizeBytes": 217172013,
      "sha256": "3cc3...",          // opcional
      "downloadUrl": "https://github.com/.../OpenRCT2-v0.5.7-android.apk"
    }
  ]
}
```

### Campos

| Campo | Obrigatório | Notas |
|---|---|---|
| `id` | sim | usado em URLs e como chave |
| `type` | não | `apk` (padrão) ou `internal` (tela dentro do app, sem download) |
| `downloadUrl` | para `apk` | link direto do release oficial |
| `sha256` | não | se presente, o app confere após baixar |
| `packageName` | não | permite mostrar "Instalado" |
| `featured` | não | aparece no carrossel da loja |

## Adicionar um jogo

1. Confirme que a licença permite redistribuir o APK ou que é um port que exige dados do usuário.
2. Pegue a URL direta do **release oficial** e o `sha256` (o GitHub mostra o digest do asset).
3. Adicione a entrada e atualize `updated`.
4. Abra um PR ou edite direto (o app tem cache, então a mudança aparece depois de um tempo).

## Licença

O catálogo (este repositório) está sob MIT. Cada jogo/port mantém a sua própria licença,
indicada em `license`/`licenseUrl`.
