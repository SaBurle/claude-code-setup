# Manual de Comandos — PowerShell + Claude Code

Guia de referência rápida para quem está começando a usar o terminal (PowerShell) e o Claude Code. Guarde este arquivo e volte a ele sempre que esquecer um comando.

---

## 1. Navegação básica de pastas no PowerShell

O terminal fica sempre "dentro" de uma pasta. Os comandos abaixo servem para andar entre pastas e ver o que existe dentro delas.

### Ver em qual pasta eu estou
```powershell
pwd
```
Mostra o caminho completo da pasta atual (ex: `C:\Users\Samara\Claude`).

### Listar arquivos e pastas
```powershell
ls
```
ou, se preferir o nome mais tradicional do Windows:
```powershell
dir
```
Os dois fazem a mesma coisa: mostram o que tem dentro da pasta atual.

### Entrar em uma pasta
```powershell
cd nome-da-pasta
```
Exemplo:
```powershell
cd Claude
```
Se o nome da pasta tiver espaço, use aspas:
```powershell
cd "Minha Pasta"
```

### Voltar uma pasta (subir um nível)
```powershell
cd ..
```

### Voltar direto para a pasta do usuário
```powershell
cd ~
```

### Criar uma pasta nova
```powershell
mkdir nome-da-pasta
```
Exemplo:
```powershell
mkdir projeto-novo
```

### Deletar uma pasta ⚠️
```powershell
Remove-Item nome-da-pasta -Recurse
```
**Cuidado:** isso apaga a pasta e tudo o que está dentro dela, sem pedir confirmação e sem ir para a lixeira. Não tem "desfazer". Confira bem o nome da pasta antes de apertar Enter.

Se quiser que o PowerShell pergunte antes de apagar cada item, use:
```powershell
Remove-Item nome-da-pasta -Recurse -Confirm
```

### Deletar um arquivo
```powershell
Remove-Item nome-do-arquivo.txt
```
Mesmo aviso: não vai para a lixeira, é definitivo.

---

## 2. Como interagir com o Claude Code

### A diferença entre "pedido livre" e "comando slash"

- **Pedido em linguagem natural**: você escreve o que quer, como se estivesse conversando ou mandando mensagem para uma pessoa. Exemplo: `crie um arquivo README explicando este projeto`. O Claude interpreta o pedido e decide o que fazer.
- **Comando slash** (`/algumacoisa`): é um atalho fixo, que sempre faz a mesma ação predefinida. Exemplo: `/clear` sempre limpa a conversa, não importa o que você escreva depois.

Resumindo: se você quer que o Claude *pense* e resolva algo, escreva normalmente. Se você quer executar uma ação específica e conhecida, use um comando `/slash`.

### Onde digitar cada coisa

Existe um único campo de texto na tela do Claude Code — é ali que você digita **tanto** pedidos livres **quanto** comandos slash. A diferença é só o `/` no começo:

```
Preciso de uma função que valide CPF
```
```
/clear
```

### Como abrir uma sessão do Claude Code

No terminal (PowerShell), dentro da pasta do seu projeto, digite:
```powershell
claude
```
Isso abre a sessão interativa do Claude Code naquela pasta.

### Como fechar/sair de uma sessão

Aperte:
```
Ctrl+C
```
duas vezes seguidas. A primeira vez avisa que você está saindo; a segunda confirma e fecha.

### Como interromper uma ação em andamento

Se o Claude estiver executando algo e você quiser pará-lo (sem fechar a sessão inteira), aperte:
```
Esc
```
Isso cancela a ação atual, mas mantém a conversa aberta para você continuar dando instruções.

---

## 3. Comandos slash nativos essenciais

| Comando | O que faz |
|---|---|
| `/init` | Analisa o projeto na pasta atual e cria um arquivo `CLAUDE.md` com informações sobre o código, para o Claude "lembrar" do contexto em sessões futuras. |
| `/clear` | Apaga o histórico da conversa atual e começa do zero (útil quando a conversa ficou longa ou mudou de assunto). |
| `/compact` | Resume a conversa atual para economizar espaço, mas mantém o contexto importante (diferente do `/clear`, que apaga tudo). |
| `/status` | Mostra informações sobre a sessão atual: modelo em uso, configurações, etc. |
| `/help` | Mostra ajuda geral sobre como usar o Claude Code. |
| `/login` | Faz login (ou troca de conta) na sua conta Claude/Anthropic. |

---

## 4. Como usar comandos personalizados (slash commands que você mesma cria)

Você pode criar seus próprios comandos `/slash`, que funcionam como "atalhos" para pedidos que você usa com frequência.

**Como funciona:** cada comando personalizado é um arquivo de texto guardado em uma pasta específica de comandos do Claude Code. Quando você digita `/nome-do-comando`, o Claude lê esse arquivo e segue as instruções escritas nele.

**Exemplo prático:** este próprio manual foi gerado a partir de um comando personalizado chamado `/manual-comandos`. Ao digitar:
```
/manual-comandos
```
o Claude leu um arquivo com instruções detalhadas (o que incluir, como organizar, para quem escrever) e gerou este documento automaticamente — sem eu precisar reescrever o pedido inteiro toda vez.

**Vantagem:** em vez de digitar um pedido longo e detalhado sempre que precisar da mesma coisa, você cria o comando uma vez e depois só digita `/nome-do-comando` sempre que quiser repetir aquela tarefa.

### Comando coringa: /add-prompt

Para pedidos pontuais que não vão se repetir (ou seja, você não quer criar um comando novo para cada um), existe o comando `/add-prompt`.

#### Como funciona

1. Abra o arquivo do comando:
   ```powershell
   notepad $HOME\.claude\commands\add-prompt.md
   ```
2. Apague o conteúdo anterior e cole o pedido novo do momento.
3. Salve e feche o Notepad.
4. Dentro de uma sessão do Claude Code, digite:
   ```
   /add-prompt
   ```

#### Diferença importante

- **Comandos fixos** (ex: `/eng-prompt`, `/consultor-financeiro`) — usados várias vezes, o conteúdo não muda.
- **`/add-prompt`** — descartável, você reescreve o conteúdo a cada pedido novo.

---

## 5. Conexão com Git e GitHub

### Como pedir para o Claude Code inicializar um repositório Git

Basta pedir em linguagem natural, dentro da sessão do Claude Code:
```
inicialize um repositório Git nesta pasta
```
O Claude vai rodar o comando `git init` para você.

### Como verificar se uma pasta já é um repositório Git

Peça:
```
verifique se esta pasta já é um repositório Git
```
Ou, se quiser fazer você mesma no terminal:
```powershell
git status
```
Se aparecer uma mensagem de erro dizendo que não é um repositório, significa que ainda não foi inicializado.

### Como autenticar no GitHub

No terminal, rode:
```powershell
gh auth login
```
Isso abre um passo a passo (geralmente pelo navegador) para conectar sua conta do GitHub à ferramenta `gh` (GitHub CLI). Você só precisa fazer isso uma vez por computador.

### Como pedir para o Claude Code criar um repositório no GitHub e enviar o código (push)

Depois de autenticado com `gh auth login`, peça em linguagem natural:
```
crie um repositório no GitHub para este projeto e envie o código (push)
```
O Claude vai usar os comandos do Git e do `gh` para:
1. Criar o repositório remoto no GitHub.
2. Conectar a pasta local a esse repositório.
3. Enviar (`git push`) os arquivos.

**Dica de segurança:** ações como criar repositórios públicos ou dar push costumam pedir sua confirmação antes de executar — é normal e esperado que o Claude pergunte antes de fazer algo que afeta o GitHub de verdade.

---

## 6. Meus Caminhos

### Organização de pastas

Toda documentação/manual pessoal fica direto na pasta `Claude`.
Todo projeto novo (com código e seu próprio git) deve ser criado dentro de uma subpasta `Projetos`.

### Exemplo para criar um projeto novo

```powershell
mkdir C:\Users\Samara\Claude\Projetos\nome-do-projeto
cd C:\Users\Samara\Claude\Projetos\nome-do-projeto
claude
```

### Se quiser usar num projeto que já existe

```powershell
cd C:\Users\Samara\Claude\Projetos\teste-claude-code
claude
```

### Se quiser usar na pasta de manuais

```powershell
cd C:\Users\Samara\Claude
claude
```

### Se quiser testar uma persona em pasta nova

```powershell
mkdir C:\Users\Samara\Claude\Projetos\projeto-novo
cd C:\Users\Samara\Claude\Projetos\projeto-novo
claude
```

---

## Resumo rápido (cola de bolso)

| Quero... | Comando |
|---|---|
| Ver onde estou | `pwd` |
| Ver arquivos da pasta | `ls` ou `dir` |
| Entrar numa pasta | `cd nome-da-pasta` |
| Voltar uma pasta | `cd ..` |
| Criar pasta | `mkdir nome` |
| Apagar pasta (⚠️ cuidado) | `Remove-Item nome -Recurse` |
| Apagar arquivo (⚠️ cuidado) | `Remove-Item arquivo` |
| Abrir o Claude Code | `claude` |
| Fechar o Claude Code | `Ctrl+C` (duas vezes) |
| Parar uma ação em andamento | `Esc` |
| Limpar a conversa | `/clear` |
| Resumir a conversa | `/compact` |
| Documentar o projeto | `/init` |
| Ver status da sessão | `/status` |
| Pedir ajuda | `/help` |
| Fazer login | `/login` |
| Login no GitHub | `gh auth login` |
