# Manual de Comandos — PowerShell + Claude Code

Guia de referência rápida para quem está começando a usar o terminal (PowerShell) e o Claude Code. Guarde este arquivo e volte a ele sempre que esquecer um comando.

## Sumário

1. PowerShell
   1.1 Navegação de pastas
   1.2 Interagir com o Claude Code
2. Claude Code
   2.0 Instalação
   2.1 Comandos slash nativos
   2.2 Comandos personalizados
   2.3 Git e GitHub
3. Git e GitHub
   3.1 Checklist de fim de sessão
4. Notepad
   4.1 Atalhos e Comandos
5. E-mail
   5.1 Plus Addressing
6. Meus Caminhos
7. Resumo rápido (cola de bolso)

---

## 1. PowerShell

### 1.1 Navegação de pastas

O terminal fica sempre "dentro" de uma pasta. Os comandos abaixo servem para andar entre pastas e ver o que existe dentro delas.

| Comando | O que faz |
|---|---|
| `pwd` | Mostra o caminho completo da pasta atual (ex: `C:\Users\Samara\Claude`). |
| `ls` | Lista arquivos e pastas da pasta atual. |
| `dir` | Mesma coisa que `ls` — nome mais tradicional do Windows. |
| `cd nome-da-pasta` | Entra na pasta indicada. Exemplo: `cd Claude`. Se o nome tiver espaço, use aspas: `cd "Minha Pasta"`. |
| `cd Claude\Projetos\teste-claude-code` | Entra direto em várias subpastas em sequência (`Claude` → `Projetos` → `teste-claude-code`), em um único comando. |
| `cd ..` | Volta uma pasta (sobe um nível). |
| `cd ~` | Volta direto para a pasta do usuário. |
| `mkdir nome-da-pasta` | Cria uma pasta nova. Exemplo: `mkdir projeto-novo`. |
| `Remove-Item nome-da-pasta -Recurse` | ⚠️ Apaga a pasta e tudo o que está dentro dela, sem pedir confirmação e sem ir para a lixeira. Não tem "desfazer" — confira bem o nome antes de apertar Enter. |
| `Remove-Item nome-da-pasta -Recurse -Confirm` | Mesma coisa, mas pede confirmação antes de apagar cada item. |
| `Remove-Item nome-do-arquivo.txt` | Apaga um arquivo. Mesmo aviso: não vai para a lixeira, é definitivo. |

### 1.2 Interagir com o Claude Code

#### A diferença entre "pedido livre" e "comando slash"

- **Pedido em linguagem natural**: você escreve o que quer, como se estivesse conversando ou mandando mensagem para uma pessoa. Exemplo: `crie um arquivo README explicando este projeto`. O Claude interpreta o pedido e decide o que fazer.
- **Comando slash** (`/algumacoisa`): é um atalho fixo, que sempre faz a mesma ação predefinida. Exemplo: `/clear` sempre limpa a conversa, não importa o que você escreva depois.

Resumindo: se você quer que o Claude *pense* e resolva algo, escreva normalmente. Se você quer executar uma ação específica e conhecida, use um comando `/slash`.

#### Onde digitar cada coisa

Existe um único campo de texto na tela do Claude Code — é ali que você digita **tanto** pedidos livres **quanto** comandos slash. A diferença é só o `/` no começo:

```
Preciso de uma função que valide CPF
```
```
/clear
```

#### Comandos e atalhos essenciais

| Comando / Atalho | O que faz |
|---|---|
| `claude` | No terminal, dentro da pasta do seu projeto: abre a sessão interativa do Claude Code naquela pasta. |
| `Ctrl+C` (duas vezes) | Fecha/sai da sessão atual — a primeira vez avisa que você está saindo, a segunda confirma e fecha. |
| `Esc` | Se o Claude estiver executando algo, interrompe a ação em andamento sem fechar a sessão inteira. |
| `Shift+Tab` | Alterna o modo de permissão da conversa (negar / aprovar automaticamente / aprovar a cada turno). |
| `Ctrl+Tab` | Completa a frase sugerida no campo, para você enviar sem precisar redigitar. |

---

## 2. Claude Code

### 2.0 Instalação

Passo a passo para instalar o Claude Code do zero no Windows, via PowerShell, até a primeira sessão autenticada.

| Comando | O que faz |
|---|---|
| `irm https://claude.ai/install.ps1 \| iex` | Instala o Claude Code usando o instalador nativo. |
| `powershell -ExecutionPolicy Bypass -File install.ps1` | Alternativa caso a política de execução do PowerShell bloqueie o script do instalador. |
| `[Environment]::SetEnvironmentVariable("PATH", $env:PATH + ";C:\Users\<usuário>\.local\bin", "User")` | Adiciona o Claude Code ao PATH, caso o instalador avise "not in your PATH". Troque `<usuário>` pelo seu nome de usuário do Windows. |
| `claude --version` | Verifica se a instalação funcionou. Rode em um terminal novo. |
| `claude doctor` | Roda o diagnóstico completo da instalação. |
| `claude auth login` | Autentica sua conta Claude/Anthropic. |
| `claude` | Inicia a primeira sessão interativa, já autenticada. |

**Importante:** depois de mexer no PATH (passo do `[Environment]::SetEnvironmentVariable`), feche e reabra o terminal antes de continuar — a mudança só é reconhecida numa sessão nova.

**Checklist final (rodando `claude doctor`):**
- `Running: native`
- Path correto
- `Remote Control: signed in`

### 2.1 Comandos slash nativos

| Comando | O que faz |
|---|---|
| `/init` | Analisa o projeto na pasta atual e cria um arquivo `CLAUDE.md` com informações sobre o código, para o Claude "lembrar" do contexto em sessões futuras. |
| `/clear` | Apaga o histórico da conversa atual e começa do zero (útil quando a conversa ficou longa ou mudou de assunto). |
| `/compact` | Resume a conversa atual para economizar espaço, mas mantém o contexto importante (diferente do `/clear`, que apaga tudo). |
| `/status` | Mostra informações sobre a sessão atual: modelo em uso, configurações, etc. |
| `/help` | Mostra ajuda geral sobre como usar o Claude Code. |
| `/login` | Faz login (ou troca de conta) na sua conta Claude/Anthropic. |
| `/btw` | Faz uma pergunta rápida paralela sem interromper o trabalho atual do Claude Code. |

### 2.2 Comandos personalizados

Você pode criar seus próprios comandos `/slash`, que funcionam como "atalhos" para pedidos que você usa com frequência.

**Como funciona:** cada comando personalizado é um arquivo de texto guardado em uma pasta específica de comandos do Claude Code. Quando você digita `/nome-do-comando`, o Claude lê esse arquivo e segue as instruções escritas nele.

**Exemplo prático:** este próprio manual foi gerado a partir de um comando personalizado chamado `/manual-comandos`. Ao digitar:
```
/manual-comandos
```
o Claude leu um arquivo com instruções detalhadas (o que incluir, como organizar, para quem escrever) e gerou este documento automaticamente — sem eu precisar reescrever o pedido inteiro toda vez.

**Vantagem:** em vez de digitar um pedido longo e detalhado sempre que precisar da mesma coisa, você cria o comando uma vez e depois só digita `/nome-do-comando` sempre que quiser repetir aquela tarefa.

#### Como abrir e editar um comando

Todo comando personalizado é um arquivo `.md` guardado na pasta de comandos. Para criar ou editar qualquer um deles, abra o arquivo correspondente no Notepad:

```powershell
notepad $HOME\.claude\commands\NOME-DO-COMANDO.md
```

Troque `NOME-DO-COMANDO` pelo nome do comando desejado. Por exemplo, para editar o coringa `/add-prompt`:

```powershell
notepad $HOME\.claude\commands\add-prompt.md
```

Escreva ou substitua o prompt dentro do arquivo, salve, feche o Notepad e digite `/add-prompt` em qualquer sessão do Claude Code.

#### Comandos disponíveis

| Comando | O que faz |
|---|---|
| `/add-prompt` | Comando coringa para pedidos pontuais que não vão se repetir. |
| `/manual-comandos` | Gera o manual de referência em Markdown. |
| `/manual-html` | Converte o manual em página HTML navegável. |
| `/doc-setup` | Gera o README com o setup pessoal do Claude Code. |
| `/todo-app` | Cria o projeto de teste (lista de tarefas). |
| `/eng-prompt` | Ativa o protocolo de engenheiro de prompt (backlog, confirmação em etapas, plano antes de executar). |
| `/consultor-financeiro` | Ativa revisão de lógica financeira/contábil. |
| `/advogado-lgpd` | Ativa revisão de conformidade LGPD/proteção de dados. |
| `/marketing` | Ativa apoio de copywriting e marketing. |
| `/revisor-qa` | Ativa revisão crítica de código como QA. |
| `/recrutador-tecnico` | Ativa avaliação honesta de currículo/portfólio como recrutador técnico. |

### 2.3 Git e GitHub

**Observação:** o Claude Code não fica travado na pasta onde a sessão foi aberta. Ao pedir para ele fazer commit e push (em linguagem natural, sem precisar digitar comandos git manualmente), ele investiga sozinho o ambiente — busca arquivos, identifica o repositório correto dentro da árvore de pastas — e executa `git add`, `commit` e `push` corretamente, mesmo que a sessão tenha sido iniciada numa pasta pai, fora do repositório em si.

---

## 3. Git e GitHub

| Comando | O que faz |
|---|---|
| `inicialize um repositório Git nesta pasta` | Pedido em linguagem natural, dentro da sessão do Claude Code: o Claude roda o comando `git init` para você. |
| `verifique se esta pasta já é um repositório Git` | Pedido em linguagem natural para o Claude conferir se a pasta atual já é um repositório Git. |
| `git status` | Confere você mesma, direto no terminal. Se aparecer uma mensagem de erro dizendo que não é um repositório, significa que ainda não foi inicializado. |
| `gh auth login` | Abre um passo a passo (geralmente pelo navegador) para conectar sua conta do GitHub à ferramenta `gh` (GitHub CLI). Só precisa fazer isso uma vez por computador. |
| `crie um repositório no GitHub para este projeto e envie o código (push)` | Pedido em linguagem natural (depois de autenticada com `gh auth login`): o Claude usa os comandos do Git e do `gh` para criar o repositório remoto no GitHub, conectar a pasta local a ele e enviar (`git push`) os arquivos. |

**Dica de segurança:** ações como criar repositórios públicos ou dar push costumam pedir sua confirmação antes de executar — é normal e esperado que o Claude pergunte antes de fazer algo que afeta o GitHub de verdade.

### 3.1 Checklist de fim de sessão

| Comando | O que faz |
|---|---|
| `git status` | Verifica se há arquivos modificados ou não rastreados. |
| `git add .` | Adiciona as alterações pendentes. |
| `git commit -m "mensagem"` | Registra o commit. |
| `git push` | Envia para o repositório remoto no GitHub. |
| `Everything up-to-date` | Confirme o retorno: essa mensagem ou um push bem-sucedido. |

---

## 4. Notepad

### 4.1 Atalhos e Comandos

Esses são atalhos padrão do Windows/Notepad, não específicos do Claude Code. Eles são úteis no fluxo de editar arquivos `.md` (como os comandos personalizados da seção 2.2), porque colar texto diretamente no campo do Claude Code tem um bug conhecido no Windows — o workaround é abrir o arquivo no Notepad e colar lá.

| Atalho | O que faz |
|---|---|
| `Ctrl+A` | Selecionar todo o texto do arquivo |
| `Ctrl+S` | Salvar o arquivo |
| `Ctrl+V` | Colar |
| `Ctrl+C` | Copiar |
| `Ctrl+Z` | Desfazer última ação |
| `Ctrl+F` | Buscar texto dentro do arquivo |
| `Ctrl+End` | Ir para o final do arquivo |
| `Ctrl+Home` | Ir para o início do arquivo |
| `Alt+Tab` | Trocar entre janelas abertas (ex: Notepad e terminal) |

---

## 5. E-mail

### 5.1 Plus Addressing

#### Plus Addressing — criando e-mails de teste sem precisar de contas novas

**Como funciona tecnicamente:**
- O padrão se chama "plus addressing" (ou "subaddressing").
- Tudo entre o `+` e o `@` é ignorado pelo servidor de e-mail na hora de entregar a mensagem — mas fica visível no cabeçalho "Para:", então dá pra usar em filtros.
- `seuemail@gmail.com`, `seuemail+qualquercoisa@gmail.com`, `seuemail+123@gmail.com` → todos caem na mesma caixa.

**Outro truque exclusivo do Gmail (bônus):**

O Gmail também ignora pontos no nome de usuário: `saburleluz@gmail.com` e `sa.burle.luz@gmail.com` são o mesmo endereço. Isso não é padrão universal — só Gmail faz isso; o "+" já é mais amplamente suportado (Outlook, iCloud, Yahoo etc., com algumas exceções).

**Para que serve na prática:**
1. **Filtros automáticos** — criar uma regra no Gmail pra qualquer coisa com `+nomedoteste` ir direto pra uma pasta/label.
2. **Rastrear vazamentos** — usar `+nomedosite` ao se cadastrar em serviços diferentes; se começar a receber spam nesse alias específico, você sabe exatamente qual site vazou seu e-mail.
3. **Testes de desenvolvimento** — simular múltiplos "usuários" de teste sem precisar de e-mails reais separados.

**Limitação a saber:**

Alguns formulários de cadastro rejeitam o "+" por validação de e-mail malfeita, ou alguns serviços de e-mail corporativo bloqueiam por segurança. Fora isso, funciona na maioria dos lugares.

Use este mesmo truque manualmente (`seuemail+teste2@gmail.com`, `seuemail+bugX@gmail.com`) sempre que precisar simular contas diferentes de usuário durante testes de qualquer projeto.

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
cd C:\Users\Samara\Claude\Projetos\Manual
claude
```

### Se quiser testar uma persona em pasta nova

```powershell
mkdir C:\Users\Samara\Claude\Projetos\projeto-novo
cd C:\Users\Samara\Claude\Projetos\projeto-novo
claude
```

---

## 7. Resumo rápido (cola de bolso)

| Comando | Quero... |
|---|---|
| `pwd` | Ver onde estou |
| `ls` ou `dir` | Ver arquivos da pasta |
| `cd nome-da-pasta` | Entrar numa pasta |
| `cd ..` | Voltar uma pasta |
| `cd ~` | Voltar para a pasta do usuário |
| `mkdir nome` | Criar pasta |
| `Remove-Item nome -Recurse` | Apagar pasta (⚠️ cuidado) |
| `Remove-Item arquivo` | Apagar arquivo (⚠️ cuidado) |
| `claude` | Abrir o Claude Code |
| `Ctrl+C` (duas vezes) | Fechar o Claude Code |
| `Esc` | Parar uma ação em andamento |
| `Shift+Tab` | Alternar modo de permissão |
| `Ctrl+Tab` | Completar a frase sugerida no campo |
| `/clear` | Limpar a conversa |
| `/compact` | Resumir a conversa |
| `/init` | Documentar o projeto |
| `/status` | Ver status da sessão |
| `/help` | Pedir ajuda |
| `/login` | Fazer login |
| `/btw` | Fazer uma pergunta rápida sem interromper |
| `/add-prompt` | Pedido pontual coringa |
| `/manual-comandos` | Gerar o manual em Markdown |
| `/manual-html` | Converter o manual em HTML |
| `/doc-setup` | Gerar o README do setup pessoal |
| `/todo-app` | Criar o projeto de teste (to-do list) |
| `/eng-prompt` | Ativar protocolo de engenheiro de prompt |
| `/consultor-financeiro` | Ativar revisão financeira/contábil |
| `/advogado-lgpd` | Ativar revisão de conformidade LGPD |
| `/marketing` | Ativar apoio de marketing/copywriting |
| `/revisor-qa` | Ativar revisão crítica de código (QA) |
| `/recrutador-tecnico` | Ativar avaliação de currículo/portfólio |
| `inicialize um repositório Git nesta pasta` | Inicializar um repositório Git |
| `verifique se esta pasta já é um repositório Git` | Verificar se a pasta já é um repositório Git |
| `git status` | Ver status do Git |
| `gh auth login` | Login no GitHub |
| `crie um repositório no GitHub para este projeto e envie o código (push)` | Criar repositório no GitHub e enviar código |
