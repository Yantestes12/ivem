# Site Oficial e Sistema de Matrícula - GASCTPNA

Este repositório contém a aplicação web completa do **GASCTPNA**, integrada com webhooks do n8n e banco de dados Supabase / MySQL.

---

## 📁 Estrutura de Arquivos

* `index.html`: Página inicial e formulário de **Criar Acesso** (Passos 1 a 4). Ao concluir o cadastro, armazena os dados da conta no `localStorage` e redireciona para a Área do Aluno.
* `login.html`: Página de Login para usuários que já possuem conta cadastrada.
* `area_aluno.html`: Painel/Área do Participante, com o botão destacado **"Fazer Minha Matrícula"**.
* `matricula.html`: Ficha interativa de Matrícula Online (10 etapas com validações, escolha do projeto, núcleo, turno, laudo em Base64, e envio automático do `projeto_nome` e `email_conta` no Webhook).
* `GASCTPNA_matricula_supabase.sql`: Script SQL da tabela `GASCTPNA_matricula` formatado para **Supabase / PostgreSQL** (com colunas `TEXT` e campo `turma`).
* `GASCTPNA_matricula_mysql.sql`: Script SQL equivalente formatado para **MySQL / phpMyAdmin**.

---

## 🔄 Fluxo de Navegação do Usuário

1. **Cadastro**: O visitante acessa `index.html` → Preenche os dados de acesso → Salva a conta → É direcionado para `area_aluno.html`.
2. **Login**: Caso já tenha conta, clica em "Fazer Login" em `login.html` → Valida credenciais → É direcionado para `area_aluno.html`.
3. **Matrícula**: Na `area_aluno.html`, o participante clica em **"Fazer Minha Matrícula"** → É direcionado para `matricula.html`.
4. **Envio ao Webhook (n8n)**: Ao enviar a matrícula, o formulário dispara o payload completo contendo:
   - Todos os dados cadastrais e questionário de saúde.
   - `projeto_id` e `projeto_nome`.
   - `email_conta` (e-mail da conta do usuário logado).
   - Documentos/laudos convertidos em **Base64** (`documentos_base64`).

---

## 🚀 Como Subir para o GitHub e Hospedar

### 1. Inicializar o repositório Git
No terminal dentro desta pasta (`site_gasctpna`), execute:

```bash
git init
git add .
git commit -m "Inicializando site completo do GASCTPNA"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git
git push -u origin main
```

### 2. Opções de Hospedagem Gratuita

* **GitHub Pages**:
  1. Vá até o seu repositório no GitHub.
  2. Clique em **Settings** -> **Pages**.
  3. Em **Source**, selecione a branch `main` e a pasta `/ (root)`.
  4. Clique em **Save**. Em instantes seu site estará no ar!

* **Vercel / Netlify**:
  1. Conecte sua conta do GitHub na Vercel ou Netlify.
  2. Importe o repositório e clique em **Deploy**.
