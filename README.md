# Meu Setup do Claude Code

Guia de referência pessoal com a instalação, configuração e fluxos de trabalho que uso com o Claude Code no Windows.

Repositório: https://github.com/SaBurle/claude-code-setup

📖 [Manual de Comandos](MANUAL-COMANDOS.md) ([versão HTML navegável](manual.html)) — guia de referência para quem está começando com terminal/PowerShell e Claude Code.

## 1. Instalação

Instalado via PowerShell, usando o comando de instalação nativa:

```powershell
irm https://claude.ai/install.ps1 | iex
```

## 2. Login

1. Rodar o comando `claude` no terminal.
2. Escolher login via navegador.
3. Autenticar na conta que possui a assinatura (Pro/Max/Team, conforme o caso).
4. O navegador redireciona de volta e a sessão fica autenticada no terminal.

## 3. Problema conhecido: colar texto no Windows

**Bug:** colar texto (Ctrl+V) diretamente na interface do Claude Code no Windows não funciona corretamente.

**Workaround:**

1. Abrir o Notepad e colar o texto desejado nele.
2. Salvar como um arquivo `.txt` (ex: `prompt.txt`).
3. No Claude Code, pedir para ele ler o arquivo, por exemplo:
   ```
   Leia o arquivo C:\Users\Samara\prompt.txt e use o conteúdo como instrução.
   ```
4. O Claude Code lê o conteúdo do arquivo normalmente, contornando o bug de colar direto na interface.

## 4. Criando comandos personalizados (slash commands)

1. Criar a pasta de comandos (se ainda não existir):
   ```powershell
   mkdir $HOME\.claude\commands
   ```
2. Dentro dela, criar um arquivo `.md` com o nome do comando desejado. Exemplo: `resumir.md` vira o comando `/resumir`.
3. Colar o prompt desejado dentro do arquivo `.md`.
4. Usar o comando em qualquer sessão do Claude Code digitando `/nome-do-arquivo`.

Exemplo:

```powershell
notepad $HOME\.claude\commands\resumir.md
```

Dentro do arquivo:

```markdown
Resuma o conteúdo abaixo em tópicos curtos e objetivos.
```

Depois, em qualquer sessão: `/resumir`

## 5. Comandos slash nativos úteis

| Comando    | Para que serve                                                        |
|------------|-------------------------------------------------------------------------|
| `/init`    | Gera um `CLAUDE.md` inicial documentando o projeto/codebase atual       |
| `/clear`   | Limpa o histórico da conversa atual                                     |
| `/compact` | Compacta o contexto da conversa para liberar espaço, mantendo o essencial |
| `/status`  | Mostra o status da sessão atual (modelo, permissões, uso, etc.)         |

## 6. Subindo um projeto para o GitHub direto pelo Claude Code

1. Pedir para o Claude Code inicializar o Git e criar o repositório local:
   ```
   Inicialize o Git nesta pasta e prepare o primeiro commit.
   ```
2. Instalar o GitHub CLI (`gh`), se ainda não estiver instalado:
   ```powershell
   winget install --id GitHub.cli
   ```
3. Autenticar no GitHub:
   ```powershell
   gh auth login --web -h github.com
   ```
4. Deixar o Claude Code criar o repositório remoto e fazer o push:
   ```
   Crie o repositório no GitHub e suba o código (git push).
   ```

O Claude Code cuida do `git init`, `git add`, `git commit`, `gh repo create` e `git push` a partir desses pedidos.
