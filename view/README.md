# Plano de Treino Semanal — PWA (registro manual)

## Como usar

### 1. Hospedar os arquivos
Coloque os arquivos em qualquer host estático:
- **Vercel** (recomendado): `npx vercel` na pasta
- **Netlify**: arraste a pasta em netlify.com/drop
- **GitHub Pages**: suba para um repositório público

> O app precisa de HTTPS para funcionar como PWA instalável (no navegador comum, funciona igual sem HTTPS).

---

### 2. Registrar uma corrida

1. Abra o app no navegador
2. Clique em **+ Registrar corrida** no topo (ou no botão **+ corrida** dentro de um card de dia — já vem com a data daquele dia preenchida)
3. Preencha:
   - **Data**
   - **Tipo**: Corrida, Corrida trail ou Outro treino
   - **Distância (km)**
   - **Tempo** no formato `mm:ss` (ex: `28:30`) ou `h:mm:ss` (ex: `1:05:20`)
   - **Elevação (m)** — opcional
   - **Nome** — opcional
4. Clique em **Salvar**

O dia da semana correspondente é marcado como concluído automaticamente (se for um dia de corrida no plano), e a atividade aparece no card, no histórico da semana e nas estatísticas do mês/evolução.

Para editar ou remover uma corrida já registrada, use os ícones ✎ e × na lista de atividades da semana.

---

### 3. Instalar como PWA

**No celular (Android/iOS)**:
- Abra no Chrome/Safari → menu → "Adicionar à tela inicial"

**No desktop (Chrome)**:
- Clique no ícone de instalação na barra de endereço

---

## Funcionalidades

- 🎯 Plano de corrida progressivo de 4 semanas (meta 5:40 → 5:20 min/km), com pace, treino e força ajustados automaticamente a cada semana a partir de uma data de início configurável (botão 🎯 no cabeçalho)
- ✅ Checklist semanal de treinos
- 🍩 Gráfico rosquinha de progresso
- 🏃 Registro manual de corridas (distância, tempo, elevação) — sem depender de nenhum app externo
- ✔️ Marcação automática de dias de corrida quando você registra uma atividade na data certa
- 📊 Distância, pace e tempo nos cards
- 📈 Histórico de atividades da semana, com edição e remoção
- 📅 Estatísticas mensais (km, tempo, elevação)
- 📈 Gráficos de evolução de pace e km nas últimas 8 semanas
- 🌙 Modo escuro / claro
- 📱 Instalável como PWA
- 💾 Dados salvos localmente (localStorage) — nada é enviado para nenhum servidor

---

## Arquivos

```
tartaga/
├── index.html    ← App principal
├── manifest.json ← Config PWA
├── sw.js         ← Service Worker (offline)
└── README.md
```
