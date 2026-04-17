# Publicação GitHub Pages · Life Code

Guia passo a passo para publicar a apresentação oficial em URL gratuita, permanente, acessível em TV, desktop e mobile.

O commit inicial já foi feito localmente (ver `git log`). Falta apenas criar o repositório remoto e conectar.

---

## 1. Criar repositório no GitHub (~2 min)

1. Acessar https://github.com/new (logar com sua conta GitHub — se não tem, criar em https://github.com/signup)
2. Preencher:
   - **Repository name**: `the-beat-life-code`
   - **Description**: `Apresentacao oficial Life Code · The Beat Life Club · plano premium para 100 membros`
   - **Visibility**: Public (GitHub Pages free exige público)
   - **NÃO marcar** "Add a README" nem "Add .gitignore" (já temos locais)
3. Clicar em **Create repository**

O GitHub vai mostrar uma página com comandos. Ignora tudo e usa os comandos abaixo.

---

## 2. Conectar repositório local ao remoto (~1 min)

Abre Git Bash e roda:

```bash
cd "C:/Users/Usuario/projetos/life-code-oficial"

# Substituir {SEU-USUARIO-GITHUB} pelo seu username real
git remote add origin https://github.com/{SEU-USUARIO-GITHUB}/the-beat-life-code.git

# Primeira publicacao
git push -u origin main
```

Na primeira vez vai pedir autenticação GitHub:
- **Username**: seu username GitHub
- **Password**: use um **Personal Access Token (PAT)**, não a senha da conta

**Como gerar PAT** (se não tem):
1. https://github.com/settings/tokens
2. Generate new token → Generate new token (classic)
3. Note: `life-code-push`, Expiration: `90 days`
4. Scopes: marcar apenas `repo`
5. Generate token → **copiar o token** (só aparece uma vez)
6. Usar esse token como "password" quando o git pedir

Alternativa mais simples: instalar **GitHub CLI** (`gh`) e rodar `gh auth login` uma vez. Aí `git push` funciona sem token.

---

## 3. Ativar GitHub Pages (~1 min)

1. No GitHub, ir para o repositório `the-beat-life-code`
2. Settings (aba no topo)
3. Pages (menu lateral esquerdo)
4. Em **Source**, selecionar:
   - Branch: `main`
   - Folder: `/ (root)`
5. Save

O GitHub vai começar o deploy. Em 1-3 minutos, a URL aparece acima com "Your site is live at:"

**URL resultante**:
```
https://{SEU-USUARIO-GITHUB}.github.io/the-beat-life-code/life-code-oficial.html
```

---

## 4. Testar a URL pública

1. Copiar a URL
2. Abrir em navegador anônimo (para testar sem cache)
3. Verificar:
   - 12 slides renderizam
   - Scroll vertical com snap funciona
   - Pressionar **F** entra em fullscreen
   - **Setas ↑↓** navegam slides
   - **PageUp/PageDown** também navegam
   - Imagens carregam (podem demorar 2-3s na primeira carga — CDN do GitHub leva tempo pra popular cache)
4. Testar em celular (abrir mesma URL)

Se tudo funcionar: **publicação oficial completa.**

---

## 5. Tag da versão oficial

```bash
cd "C:/Users/Usuario/projetos/life-code-oficial"
git tag -a v1.0.0 -m "Versao oficial 1.0.0 - 17 de abril de 2026"
git push origin v1.0.0
```

No GitHub, a tag aparece em Releases → Create release (opcional, para adicionar changelog visível).

---

## 6. Workflow de atualizações futuras

Quando precisar atualizar o deck:

```bash
cd "C:/Users/Usuario/projetos/life-code-oficial"

# Editar life-code-oficial.html (aqui, não no Drive)

# Commit e push
git add life-code-oficial.html
git commit -m "fix: descricao curta do ajuste"
git push

# Sincronizar com Drive (manual, opcional)
cp life-code-oficial.html "G:/Meu Drive/The Beat Life Club/design/projeto-life-code/layouts-life-code/life-code-oficial.html"

# Se for release, tag
git tag v1.1.0 && git push --tags

# Regerar PDF (opcional, via Chrome headless - ver README.md)
```

GitHub Pages redeploya automaticamente ~1 min após cada push.

---

## 7. Recovery · se algo quebrar

**Cenário 1**: arquivo quebrou localmente
```bash
cd "C:/Users/Usuario/projetos/life-code-oficial"
git restore life-code-oficial.html  # volta ao último commit
```

**Cenário 2**: perda total da pasta local
```bash
cd "C:/Users/Usuario/projetos/"
git clone https://github.com/{SEU-USUARIO}/the-beat-life-code.git life-code-oficial
```

**Cenário 3**: repo do GitHub quebrou ou foi deletado
- Recuperar cópia local ou snapshot no Google Drive
- `git remote remove origin && git remote add origin {novo-url} && git push -u origin main`

**Cenário 4**: perda total (local + GitHub + cópia)
- Abrir Drive web → life-code-oficial.html → botão direito → Gerenciar versões → escolher versão a restaurar

Quatro camadas de recovery. É improvável perder tudo ao mesmo tempo.

---

## 8. Alternativa · Cloudflare Pages (se preferir repo privado)

Caso você prefira que o repositório seja privado (mas ainda URL pública e gratuita):

1. Criar conta em https://pages.cloudflare.com (gratuita)
2. Connect Git → GitHub (mesmo que seja repo privado)
3. Selecionar `the-beat-life-code`
4. Build command: (deixar vazio — site estático)
5. Output directory: `/`
6. Deploy

URL resultante: `the-beat-life-code.pages.dev`

Vantagens Cloudflare Pages vs GitHub Pages:
- Permite repo privado (grátis)
- CDN muito mais rápido globalmente
- Deploy em ~30s
- Preview deployments automáticos para branches

Pode usar uma das duas. GitHub Pages é mais clássico e direto.
