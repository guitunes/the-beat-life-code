# Life Code · Apresentação Oficial

Deck editorial do plano premium Life Code do The Beat Life Club. Formato 1920×1080 landscape, 12 slides, apresentação comercial face a face para 100 membros.

---

## Estrutura da pasta

```
layouts-life-code/
├── life-code-oficial.html    ← ARQUIVO PRINCIPAL · read-only
├── life-code-oficial.pdf     ← Export oficial para offline/impressão
├── assets/                   ← 13 imagens essenciais (não editar)
├── review/                   ← Documentação editorial (direção de arte, marca, tipografia)
├── README.md                 ← Este arquivo
├── .gitignore                ← Regras de versionamento
└── _backup-limpeza/          ← NÃO REMOVER · arquivos históricos e snapshots
    ├── snapshots/            ← Versões datadas (recovery)
    ├── pipeline-antigo-tv-slides/   ← Script Python merger + 16 slides individuais desatualizados
    ├── assets-archive/       ← Arquivo original _archive
    └── assets-nao-usados/    ← 16 imagens testadas e descartadas ao longo do projeto
```

---

## URL pública

A apresentação está publicada em:

> **https://{usuario-github}.github.io/the-beat-life-code/life-code-oficial.html**

URL estável, gratuita, hospedada em GitHub Pages. Acesso:
- TV/desktop (recomendado para apresentação)
- Mobile (visualização reduzida, use pinch-zoom)
- Sem sleep, sem pagamento, sempre no ar

Para apresentar comercialmente:
1. Abrir a URL em navegador (Chrome recomendado)
2. Pressionar **F** para fullscreen
3. **Setas ↑↓** ou **PageUp/PageDown** para navegar entre slides
4. **Home** volta ao s01, **End** vai ao s12
5. Em mobile, touch swipe vertical funciona

---

## PROTOCOLO DE SEGURANÇA

### Regra 1 · Arquivo oficial é read-only

O `life-code-oficial.html` tem atributo **read-only** ativo no Windows. Qualquer edição acidental é bloqueada pelo sistema.

**Para alterar o deck legitimamente**, o fluxo é:

1. Duplicar o arquivo: `life-code-oficial.html` → `life-code-rascunho-YYYY-MM-DD.html`
2. Editar a cópia rascunho
3. Validar (abrir no browser, navegar os 12 slides)
4. Promover: remover read-only do oficial, sobrescrever, aplicar read-only de novo
5. Commit no git + push (atualiza URL pública automaticamente)
6. Tag release: `git tag v1.X.0 && git push --tags`

### Regra 2 · Snapshot antes de mudanças grandes

Antes de qualquer refatoração, criar snapshot em:
```
_backup-limpeza/snapshots/YYYY-MM-DD-descricao/
```

Copiar o `life-code-oficial.html` e `life-code-oficial.pdf` atuais. É seguro de baixo custo e salva o deck se algo der errado.

### Regra 3 · Três camadas de backup

Em ordem de velocidade de recovery:
1. **Git local** (no computador) · `git log` para histórico, `git checkout {hash}` para voltar
2. **GitHub remote** (cloud) · `git pull` ou clone do zero se perder tudo
3. **Google Drive version history** · 100 versões, 30 dias · botão direito no arquivo → Gerenciar versões

Se perder o arquivo no Drive: clonar o repo GitHub.
Se perder o repo GitHub: usar Google Drive version history.
Se perder ambos: `_backup-limpeza/snapshots/` locais.

### Regra 4 · Nunca dois chats editando o mesmo arquivo

Aprendizado real do projeto: **dois chats de Claude Code rodando em paralelo no mesmo arquivo não compartilham estado**. Um sobrescreve o trabalho do outro sem aviso. Recovery foi via Google Drive version history.

Regra operacional:
- Um chat, um arquivo por vez
- Se precisar trabalho paralelo, dividir por arquivo (um chat em HTML, outro em CSS externo)
- Ao iniciar novo chat que toca arquivo compartilhado, sempre ler o arquivo antes de editar

---

## Regerar o PDF

Quando houver atualização no HTML, gerar novo PDF via Chrome headless:

```bash
"/c/Program Files/Google/Chrome/Application/chrome.exe" \
  --headless=new --disable-gpu --no-sandbox --hide-scrollbars \
  --virtual-time-budget=15000 --run-all-compositor-stages-before-draw \
  --print-to-pdf="C:/Users/Usuario/AppData/Local/Temp/life-code-oficial.pdf" \
  --no-pdf-header-footer \
  "file:///G:/Meu%20Drive/The%20Beat%20Life%20Club/design/projeto-life-code/layouts-life-code/life-code-oficial.html"
```

Depois copiar:
```bash
cp "C:/Users/Usuario/AppData/Local/Temp/life-code-oficial.pdf" \
   "G:/Meu Drive/The Beat Life Club/design/projeto-life-code/layouts-life-code/life-code-oficial.pdf"
```

O download direto para o Google Drive dá erro de "Acesso negado" por conflito de sync — sempre gerar em local temp e copiar depois.

---

## Reuso como referência para outras peças

O deck estabelece um **sistema visual reutilizável**. Outros projetos podem copiar trechos sem tocar no oficial:

### Classes CSS disponíveis
- `.pg--noir-framed` · passe-partout light para spreads noir
- `.map-paper-grain` · textura de papel sobre fundos claros
- `.map-light-wash` · luz aurum radial canto superior
- `.map-sigil-hero` · sigilo watermark 900px sangrando
- `.tv-caption-fig` · caption museu `Fig. N · descrição`
- `.map-atcg` · linha micro-stream editorial

### Paleta cromática
- `--noir: #0E0E12`
- `--branco-livro: #F2EDE2`
- `--aurum: #C9A96E`
- `--aurum-claro: #E6CF9A`
- `--aurum-dark: #8B6F3E`
- `--pergaminho: #E6DDD0`

### Tipografia
- Display: Cormorant Garamond italic (Google Fonts)
- Body: EB Garamond (Google Fonts)
- Mono: JetBrains Mono uppercase labels (Google Fonts)

### Técnicas aplicadas
- Typographic debossing (letterpress via 2 text-shadows)
- Double-frame CTA com corner ornaments L-shape
- Halation aurum (Kodak Portra)
- Grain film via SVG fractalNoise
- Scrims top/bottom em imagens
- Moldura hairline aurum inset

**NUNCA editar o arquivo oficial para adaptar a outros projetos.** Copiar trechos para o novo arquivo, sempre.

---

## Contato do projeto

- Proprietário: Guilherme Motta Tunes (guimottatunes@gmail.com)
- Marca: The Beat Life Club
- Produto: Life Code (plano premium · 100 membros exclusivos)
- Data de publicação oficial: 17 de abril de 2026
