# Plano de Treino Semanal — PWA + Strava

## Como usar

### 1. Hospedar os arquivos
Coloque os 3 arquivos em qualquer host estático:
- **Vercel** (recomendado): `npx vercel` na pasta
- **Netlify**: arraste a pasta em netlify.com/drop
- **GitHub Pages**: suba para um repositório público

> O app precisa de HTTPS para funcionar como PWA e para o OAuth do Strava.

---

### 2. Configurar o Strava

1. Acesse https://www.strava.com/settings/api
2. Crie um app com:
   - **App Name**: Treino Tracker (qualquer nome)
   - **Authorization Callback Domain**: seu domínio (ex: `meutreino.vercel.app`)
3. Copie o **Client ID** e **Client Secret**

---

### 3. Conectar no app

1. Abra o app no navegador
2. Clique em **Conectar Strava**
3. Cole o Client ID e Client Secret
4. Clique em **Autorizar** — você será redirecionado ao Strava
5. Após autorizar, o app sincroniza automaticamente

---

### 4. Instalar como PWA

**No celular (Android/iOS)**:
- Abra no Chrome/Safari → menu → "Adicionar à tela inicial"

**No desktop (Chrome)**:
- Clique no ícone de instalação na barra de endereço

---

## Funcionalidades

- 🎯 Plano de corrida progressivo de 4 semanas (meta 5:40 → 5:20 min/km), com pace, treino e força ajustados automaticamente a cada semana a partir de uma data de início configurável (botão 🎯 no cabeçalho)
- ✅ Checklist semanal de treinos
- 🍩 Gráfico rosquinha de progresso
- 🔶 Sincronização automática com Strava
- 🏃 Marcação automática de dias de corrida
- 📊 Distância, pace e tempo nos cards
- 📈 Histórico de atividades da semana
- 📅 Estatísticas mensais (km, tempo, elevação)
- 🌙 Modo escuro / claro
- 📱 Instalável como PWA
- 💾 Dados salvos localmente (localStorage)

---

## Arquivos

```
treino-tracker/
├── index.html    ← App principal
├── manifest.json ← Config PWA
├── sw.js         ← Service Worker (offline)
└── README.md
```
