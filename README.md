# Diário de dor de cabeça

Aplicativo web simples para registrar episódios de dor de cabeça e os remédios tomados, com um relatório por período. É um único arquivo HTML, sem instalação, sem servidor e sem dependências externas.

## Funcionalidades

### Registrar

- **Início da dor:** data e hora (já vem preenchida com o momento atual).
- **Grau da dor:** de 1 a 5 (leve, incômoda, moderada, forte, intensa).
- **Remédios tomados (opcional):** seleção múltipla, para marcar mais de um remédio no mesmo registro.
  - **Incluir novo:** digite o nome (e a dose, se quiser) e toque em **Incluir**. O remédio fica salvo na lista para os próximos registros.
  - **Excluir da lista:** toque em **Editar lista**, depois em **✕** ao lado do remédio e confirme. Os registros antigos continuam com o nome como foi gravado.
- **Comentário (opcional):** texto livre, por exemplo local da dor, gatilho ou sintomas.

### Relatório

- **Filtro de período:** últimos 7, 30 ou 90 dias, último ano, todos os registros ou datas escolhidas.
- **Resumo:** quantidade de episódios, dor média e quantos episódios tiveram remédio.
- **Gráfico:** quantidade de episódios por grau de dor.
- **Lista de registros:** data e hora, grau, remédios e comentário, com opção de excluir cada registro.

### Dados

- **Exportar CSV:** os registros do período filtrado, para abrir em planilhas.
- **Exportar backup:** todos os registros em um arquivo JSON.
- **Importar backup:** restaura ou une registros de um backup. Registros que já existem não são duplicados.

## Como usar

1. Abra o arquivo `dor-de-cabeca.html` no navegador (computador ou celular).
1. Na aba **Registrar**, preencha os dados e toque em **Salvar registro**.
1. Na aba **Relatório**, escolha o período para ver o resumo, o gráfico e os comentários.

## Publicar no GitHub Pages (grátis)

1. Suba o arquivo para um repositório no GitHub. Se quiser que o endereço seja mais curto, renomeie-o para `index.html`.
1. No repositório, acesse **Settings → Pages**.
1. Em **Build and deployment**, escolha **Deploy from a branch**, selecione a branch `main` e a pasta `/ (root)`, e salve.
1. Aguarde alguns minutos. O app ficará em `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/` (ou com `/dor-de-cabeca.html` no final, se não renomear o arquivo).

No celular, é possível adicionar o endereço à tela inicial pelo menu do navegador para abrir como se fosse um aplicativo, já com o ícone.

## Onde os dados ficam salvos

Os registros ficam **somente no navegador do aparelho** (`localStorage`). Nada é enviado para servidor, e o repositório do git guarda apenas o código do app, não os registros.

Isso tem algumas consequências:

- Os dados **não sincronizam** entre aparelhos ou navegadores diferentes. Para levar os registros para outro lugar, use **Exportar backup** e **Importar backup**.
- **Limpar os dados do navegador apaga os registros.** Faça backup de vez em quando.
- Navegar em aba anônima/privada não mantém os dados depois que a aba é fechada.

### Formato do backup

O backup é uma lista de registros em JSON:

```json
[
  {
    "id": "m1abc2de",
    "inicio": "2026-11-02T13:30:00.000Z",
    "dor": 3,
    "remedios": ["Remédio A 500 mg", "Remédio B"],
    "comentario": "Começou depois do almoço."
  }
]
```

|Campo       |Descrição                                       |
|------------|------------------------------------------------|
|`id`        |Identificador único do registro                 |
|`inicio`    |Data e hora do início, em formato ISO 8601 (UTC)|
|`dor`       |Grau da dor, de 1 a 5                           |
|`remedios`  |Lista com os remédios tomados (pode ser vazia)  |
|`comentario`|Texto livre (pode ser vazio)                    |

Backups de versões anteriores, com um único campo `remedio`, também são aceitos.

## Estrutura do projeto

```
dor-de-cabeca.html     # app completo (HTML, CSS e JavaScript)
icon.svg               # ícone vetorial (favicon do navegador)
icon-192.png           # ícone para a tela inicial (Android)
icon-512.png           # ícone grande / maskable (Android)
apple-touch-icon.png   # ícone para a tela inicial (iPhone/iPad)
manifest.webmanifest   # nome e ícones para adicionar à tela inicial
README.md              # este arquivo
```

Mantenha todos os arquivos na mesma pasta do HTML, para os ícones serem encontrados.

## Tecnologia

HTML, CSS e JavaScript puro, em um único arquivo. Usa `localStorage` para guardar os dados e respeita o modo claro/escuro do aparelho.

## Aviso

Este aplicativo serve apenas para organizar e acompanhar seus registros. Ele não faz diagnóstico nem substitui a orientação de um profissional de saúde.