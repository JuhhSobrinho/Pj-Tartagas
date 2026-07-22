# Widget Tartaga no Android — Guia KWGT

## O que você vai precisar

- App **KWGT Kustom Widget Maker** (gratuito na Play Store)
- App **KWGT Pro Key** (~R$15, necessário para widgets funcionarem na tela inicial)
- O Tartaga já hospedado no GitHub Pages

---

## Como funciona

O widget lê os dados diretamente da página `widget-data.html` do seu app via requisição HTTP. Isso significa que os dados são sempre atualizados quando o widget recarrega.

---

## Passo a passo

### 1. Instalar os apps

1. Instale **KWGT Kustom Widget Maker** na Play Store
2. Instale **KWGT Pro Key** na Play Store (desbloqueia widgets na tela inicial)

---

### 2. Criar o widget

1. Pressione e segure a tela inicial do Android
2. Toque em **Widgets**
3. Encontre **KWGT** e escolha o tamanho **4×2** (recomendado)
4. Arraste para a tela inicial
5. Toque no widget para abrir o editor

---

### 3. Configurar o widget no editor KWGT

#### Camada de fundo
1. Toque em **+** → **Shape**
2. Tipo: **Rectangle**, Corner Radius: **24**
3. Cor: `#262624`
4. Tamanho: preenche o widget inteiro

#### Título "tartaga"
1. **+** → **Text**
2. Texto: `tartaga`
3. Fonte: qualquer, tamanho 14, cor `#1D9E75`
4. Posição: canto superior esquerdo

#### Anel de progresso (círculo)
1. **+** → **Shape** → **Arc**
2. Ângulo start: `-90`, Sweep: fórmula abaixo
3. Cor: `#1D9E75`, espessura: 8
4. Fórmula do sweep:
```
$si(gv(done) / 7 * 360, 0)$
```

#### Número central
1. **+** → **Text**
2. Fórmula: `$gv(done)$`
3. Tamanho: 28, cor branca, centralizado no anel

#### Treino de hoje
1. **+** → **Text**
2. Fórmula: `$gv(today_title)$`
3. Tamanho: 14, cor `#e8e6e0`

#### Km da semana
1. **+** → **Text**
2. Fórmula: `$gv(week_km)$ km`
3. Cor: `#1D9E75`

---

### 4. Configurar as variáveis globais (Global Variables)

Esta é a parte que conecta o widget ao seu app.

1. No editor KWGT, toque no ícone de **engrenagem** (settings)
2. Vá em **Globals**
3. Crie as seguintes variáveis:

| Nome | Tipo | Valor padrão |
|------|------|-------------|
| `done` | Number | 0 |
| `total` | Number | 7 |
| `run_done` | Number | 0 |
| `str_done` | Number | 0 |
| `week_km` | Text | 0.0 |
| `today_title` | Text | Carregando... |
| `today_tag` | Text | — |
| `today_done` | Boolean | false |
| `program_week` | Number | 1 |

---

### 5. Configurar a atualização automática via Tasker

Para os dados atualizarem automaticamente, use o **Tasker** (app de automação):

1. Instale o **Tasker** na Play Store (tem período de teste gratuito)
2. Crie um novo **Profile** → **Time** → a cada 30 minutos
3. Na **Task**, adicione as ações:

**Ação 1 — HTTP Request**
- Método: GET
- URL: `https://juhhsobrinho.github.io/Pj-Tartagas/widget-data.html`
- Salvar resposta em: `%response`

**Ação 2 — JSON Parse** (repita para cada variável)
- Variável de entrada: `%response`
- Path: `done` → salva em `%done`
- Path: `today.title` → salva em `%today_title`
- Path: `weekKm` → salva em `%week_km`
- etc.

**Ação 3 — KWGT Set Variable** (repita para cada variável)
- Widget: selecione o Tartaga
- Variável: `done` → Valor: `%done`
- Variável: `today_title` → Valor: `%today_title`
- etc.

---

### Alternativa mais simples — sem Tasker

Se não quiser usar o Tasker, use o **HTTP Request nativo do KWGT**:

1. No editor KWGT → **+** → **Text**
2. Use a fórmula diretamente:
```
$br(json, "https://juhhsobrinho.github.io/Pj-Tartagas/widget-data.html", "done")$
```

Isso faz a requisição diretamente no KWGT. Substitua `done` pelo campo que quiser.

**Campos disponíveis na URL:**
- `done` — treinos concluídos (número)
- `total` — total de treinos (7)
- `percent` — porcentagem concluída
- `weekKm` — km rodados na semana
- `today.title` — treino de hoje
- `today.tag` — tag do treino de hoje
- `today.done` — se o treino de hoje foi concluído
- `runDone` / `runTotal` — corridas concluídas / total de dias de corrida (3)
- `strDone` / `strTotal` — dias de força concluídos / total de dias de força (2)
- `programWeek` — semana atual do plano de corrida (1 a 4, mostra a progressão de pace 5:40 → 5:20)

> A semana do plano (`programWeek`) é calculada a partir da data de início configurada no app (botão 🎯 no cabeçalho). Configure a mesma data lá antes de usar o widget.

---

## Visual de referência

Abra no celular para ver como o widget fica:
```
https://juhhsobrinho.github.io/Pj-Tartagas/widget-data.html
```

---

## Dicas

- O widget atualiza automaticamente quando você abre o KWGT
- Para forçar atualização: pressione e segure o widget → Edit → salve sem alterar nada
- Com o Tasker configurado, atualiza a cada 30 minutos em background
- O tamanho **4×2** na tela inicial é o ideal para mostrar todas as informações
