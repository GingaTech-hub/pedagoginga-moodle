# Pedagoginga Moodle - Guia de Onboarding para Desenvolvedores 🚀

Este repositório contém a instância do **Moodle 4.x** para o ambiente virtual de aprendizagem da **Plataforma Pedagoginga**.

Este guia reúne as instruções necessárias para que novos desenvolvedores configurem o ambiente local e sigam os padrões de customização e arquitetura do projeto.

---

## 💻 1. Configuração do Ambiente Local (Windows)

Não é necessário instalar **PHP, Apache ou MySQL** separadamente na máquina.

O projeto foi empacotado para Windows com todos os serviços necessários integrados à estrutura local.

### 📋 Passo a Passo para Iniciar

#### 1. Clonar o Repositório

```bash
git clone https://github.com/GingaTech-hub/pedagoginga-moodle.git
cd pedagoginga-moodle
```

#### 2. Iniciar os Serviços Localmente

Na raiz do projeto, dê um duplo clique no arquivo:

```text
Start Moodle.exe
```

Duas janelas do prompt/terminal serão abertas para manter o **Apache** e o **MariaDB** em execução.

> ⚠️ **Importante:** mantenha essas janelas abertas enquanto estiver desenvolvendo.

#### 3. Acessar a Plataforma

**Navegador local:**

```text
http://localhost/
```

**Acesso pela rede local (celular/outros dispositivos):**

```text
http://SEU_IP_LOCAL/
```

> Para descobrir seu IP local no Windows, execute `ipconfig` no Prompt de Comando e procure pelo endereço IPv4 da conexão de rede utilizada.

#### 4. Encerrar o Servidor

Quando terminar o desenvolvimento, dê um duplo clique no arquivo:

```text
Stop Moodle.exe
```

Isso encerrará com segurança os processos do banco de dados e do servidor web.

---

## 🎨 2. Arquitetura Visual e Diretrizes de Front-end

Para manter a consistência visual da plataforma, todas as customizações devem respeitar as especificações abaixo.

### 🎨 Paleta de Cores Oficial

| Uso | Cor | Hexadecimal |
|---|---|---|
| Azul Principal (Navbar/Banners) | Azul escuro | `#29295F` |
| Amarelo Destaque (Bordas e Elementos Ativos) | Amarelo | `#DBA20C` |
| Verde Destaque (Cards e Avisos) | Verde | `#367F30` |
| Fundo da Aplicação | Azul escuro | `#29295F` |

### 🖥️ Customizações de Layout e Tema

A estilização do layout da plataforma é aplicada diretamente sobre o tema **Boost** do Moodle utilizando **SCSS/CSS Raw**.

Entre as principais customizações estão:

- Navegação primária;
- Remoção da barra secundária;
- Contêineres em largura total (`full-width`);
- Customização do cabeçalho;
- Ajustes visuais de componentes;
- Aplicação da identidade visual da Plataforma Pedagoginga.

### 📍 Local das Configurações

No Moodle, acesse:

```text
Administração do Site
└── Aparência
    └── Temas
        └── Boost
            └── Configurações Avançadas
```

As alterações de estilo devem ser realizadas respeitando a estrutura e as diretrizes visuais existentes no projeto.

---

## ⚠️ 3. Versionamento e Segurança

### `.gitignore`

**Nunca remova ou altere as regras existentes no arquivo `.gitignore` sem uma necessidade técnica devidamente avaliada.**

O projeto possui arquivos e diretórios locais que não devem ser versionados.

Entre eles:

```text
server/
config.php
```

### 📁 `server/`

A pasta `server/` contém os binários e componentes necessários para execução local do:

- Apache;
- MariaDB;
- PHP;
- Moodle.

Essa pasta é **ignorada pelo Git** para evitar o versionamento de binários e arquivos específicos do ambiente local.

### 🔐 `config.php`

O arquivo `config.php` contém configurações locais do Moodle, incluindo informações relacionadas à conexão com o banco de dados e ao ambiente de execução.

Esse arquivo também é **ignorado pelo Git**.

> 🚨 **Nunca versione credenciais, senhas ou configurações sensíveis no repositório.**

---

# 🛠️ 4. Resolução de Problemas Comuns (Troubleshooting)

## ❌ Start Moodle.exe fecha sozinho imediatamente

### Possível causa

A porta **80** do Windows está sendo utilizada por outra aplicação.

Alguns exemplos:

- Skype;
- IIS;
- Docker;
- XAMPP;
- WAMP;
- Outro servidor web.

### Solução

Verifique qual processo está utilizando a porta 80 e encerre-o antes de iniciar o Moodle novamente.

No Prompt de Comando do Windows:

```bash
netstat -ano | findstr :80
```

O comando mostrará o PID do processo que está utilizando a porta.

Depois, identifique o processo pelo Gerenciador de Tarefas ou execute:

```bash
tasklist | findstr <PID>
```

Após liberar a porta, execute novamente:

```text
Start Moodle.exe
```

---

## ❌ Falha ao iniciar o PHP / Erros de DLL

### Possível causa

Dependências do **Microsoft Visual C++ Redistributable** podem estar ausentes ou desatualizadas.

### Solução

Baixe e instale a versão mais recente do:

**Microsoft Visual C++ Redistributable (VS16+).**

Depois da instalação, reinicie o ambiente e tente executar novamente:

```text
Start Moodle.exe
```

---

## ❌ Mudanças em CSS/Layout não aparecem na tela

O Moodle utiliza cache de temas, portanto alterações no SCSS/CSS podem não aparecer imediatamente.

### Solução

Acesse:

```text
Administração do Site
└── Aparência
    └── Temas
        └── Temas
```

E clique em:

```text
Limpar o cache de temas
```

Depois, atualize a página do navegador.

### 💡 Dica

Se necessário, faça uma atualização forçada do navegador:

**Windows/Linux:**

```text
Ctrl + F5
```

---

# 📁 5. Estrutura do Repositório

A estrutura principal esperada é:

```text
pedagoginga-moodle/
├── .gitignore
│   # Filtros para ignorar dados sensíveis,
│   # cache e arquivos do servidor local
│
├── README.md
│   # Guia de onboarding e documentação técnica
│
├── Start Moodle.exe
│   # Executável para iniciar Apache + MariaDB
│
├── Stop Moodle.exe
│   # Executável para interromper o ambiente local
│
└── server/
    # [Ignorado no Git]
    # Binários do servidor e aplicação Moodle
    │
    └── moodle/
        # Código-fonte da aplicação Moodle
        # e customizações/temas do projeto
```

---

# 🔄 6. Fluxo Básico de Desenvolvimento

Para iniciar um trabalho no projeto:

### 1. Atualizar o repositório

```bash
git pull
```

### 2. Iniciar o ambiente local

Execute:

```text
Start Moodle.exe
```

### 3. Acessar o Moodle

Abra:

```text
http://localhost/
```

### 4. Desenvolver e testar

Realize as alterações necessárias respeitando:

- A arquitetura existente;
- A identidade visual;
- As configurações do tema Boost;
- As boas práticas do Moodle;
- As regras do `.gitignore`.

### 5. Limpar o cache quando necessário

Após alterações visuais:

```text
Administração do Site
→ Aparência
→ Temas
→ Temas
→ Limpar o cache de temas
```

### 6. Versionar somente o que deve ir para o Git

Antes de realizar o commit:

```bash
git status
```

Verifique se arquivos locais, credenciais, cache ou binários não estão sendo adicionados ao commit.

### 7. Encerrar o ambiente

Ao finalizar:

```text
Stop Moodle.exe
```

---

# 🌐 7. Acesso pela Rede Local

O Moodle pode ser acessado por outros dispositivos conectados à mesma rede local.

Por exemplo:

```text
http://192.168.0.10/
```

O endereço exato depende do IP local da máquina que está executando o servidor.

Para descobrir o endereço:

```bash
ipconfig
```

Procure por:

```text
Endereço IPv4
```

### ⚠️ Possíveis bloqueios

Caso outro dispositivo não consiga acessar o Moodle, verifique:

- Se os dispositivos estão na mesma rede;
- Se o Apache está em execução;
- Se a porta 80 está liberada;
- Se o Firewall do Windows está bloqueando o Apache;
- Se o endereço IP utilizado está correto.

---

# 🧩 8. Tecnologias Principais

O ambiente local do projeto utiliza principalmente:

| Tecnologia | Função |
|---|---|
| **Moodle 4.x** | Plataforma de aprendizagem |
| **PHP** | Runtime da aplicação |
| **Apache** | Servidor web |
| **MariaDB** | Banco de dados |
| **SCSS/CSS** | Customização visual |
| **Tema Boost** | Base visual do Moodle |

Os componentes necessários para execução local são disponibilizados dentro da estrutura do projeto, evitando a necessidade de instalação manual de cada serviço.

---
# 🚨 9. Boas Práticas

### Não faça

- ❌ Não altere o `.gitignore` sem necessidade;
- ❌ Não versione `config.php`;
- ❌ Não versione a pasta `server/`;
- ❌ Não coloque senhas ou credenciais no Git;
- ❌ Não altere a identidade visual sem alinhamento com o projeto;
- ❌ Não substitua configurações existentes sem entender seu impacto.

### Faça

- ✅ Mantenha o ambiente local atualizado;
- ✅ Teste as alterações antes de criar commits;
- ✅ Limpe o cache de temas após alterações visuais;
- ✅ Verifique o `git status` antes de fazer commit;
- ✅ Mantenha a documentação atualizada;
- ✅ Siga a paleta e os padrões visuais da Pedagoginga.
---

## 🚀 Bem-vindo ao desenvolvimento da Plataforma Pedagoginga!

Este documento deve ser utilizado como ponto de partida para configurar o ambiente local e compreender os principais padrões técnicos e visuais do projeto.
