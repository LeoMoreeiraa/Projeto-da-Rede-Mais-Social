# 🌐 Rede Mais Social

> Sistema web para gestão de afiliação de voluntários e ONGs

[![Java](https://img.shields.io/badge/Java-8+-orange.svg)](https://www.oracle.com/java/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-blue.svg)](https://www.mysql.com/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

O projeto **Rede Mais Social** é uma plataforma web que conecta **candidatos, voluntários e ONGs**, gerenciando todo o processo de afiliação desde o cadastro inicial até a aprovação final. O sistema garante confiabilidade através de validações e tokens de confirmação, facilitando a participação em campanhas sociais.

---

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Tecnologias](#tecnologias)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Como Usar](#como-usar)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Arquitetura](#arquitetura)
- [Documentação](#documentação)
- [Contribuindo](#contribuindo)
- [Licença](#licença)

---

## 🎯 Sobre o Projeto

A **Rede Mais Social** foi desenvolvida como projeto acadêmico para demonstrar conceitos de:
- Desenvolvimento web full-stack
- Arquitetura MVC (Model-View-Controller)
- Integração frontend-backend
- Persistência de dados com banco relacional
- Validações e segurança básica

### Visão Geral do Processo

1. **Cadastro**: Candidato preenche formulário com dados pessoais (CPF ou CNPJ)
2. **Validação**: Sistema valida email, CPF/CNPJ e gera token de confirmação
3. **Confirmação**: Token enviado por email para validar cadastro
4. **Aprovação**: Representante analisa e aprova/rejeita solicitação
5. **Ativação**: Candidato aprovado torna-se voluntário ativo

---

## ✨ Funcionalidades

### Para Candidatos
- ✅ Cadastro como Pessoa Física (CPF) ou Pessoa Jurídica (CNPJ)
- ✅ Formulário multi-etapas (identificação → perfil → termo)
- ✅ Validação de email com token único
- ✅ Consulta de status da solicitação
- ✅ Login para retornar ao cadastro

### Para o Sistema
- ✅ Validação de email, CPF e CNPJ
- ✅ Geração automática de tokens MD5
- ✅ Envio de emails de confirmação (simulado)
- ✅ Armazenamento seguro no MySQL
- ✅ Interface responsiva e intuitiva

---

## 🛠️ Tecnologias

### Backend
- **Java 8+** - Linguagem principal
- **HttpServer** - Servidor HTTP nativo do Java
- **JDBC** - Conexão com banco de dados
- **MySQL Connector** - Driver JDBC para MySQL

### Frontend
- **HTML5** - Estrutura das páginas
- **CSS3** - Estilização e layout responsivo
- **JavaScript (ES6+)** - Interatividade e requisições AJAX

### Banco de Dados
- **MySQL 8.0** - Sistema gerenciador de banco de dados

### Arquitetura
- **MVC** - Separação de responsabilidades
- **DAO Pattern** - Acesso a dados
- **REST API** - Comunicação cliente-servidor

---

## 📦 Pré-requisitos

Antes de começar, certifique-se de ter instalado:

```bash
# Java JDK 8 ou superior
java -version

# MySQL 8.0 ou superior
mysql --version

# Git (opcional, para clonar o repositório)
git --version
```

---

## 🚀 Instalação

### 1. Clone o repositório

```bash
git clone https://github.com/LeoMoreeiraa/Projeto-da-Rede-Mais-Social.git
cd Projeto-da-Rede-Mais-Social
```

### 2. Configure o MySQL

```bash
# Inicie o serviço MySQL
sudo service mysql start

# Configure sem senha (para desenvolvimento)
sudo mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY ''; FLUSH PRIVILEGES;"

# Crie o banco de dados
mysql -u root < scriptBancoDados.txt
```

> **Nota**: Para instruções detalhadas de instalação do MySQL, consulte [INSTALACAO_MYSQL.txt](INSTALACAO_MYSQL.txt)

### 3. Execute o sistema

```bash
bash run.sh
```

O servidor será iniciado em: **http://localhost:8080**

---

## 💻 Como Usar

### Acesso Rápido

Abra seu navegador e acesse:
```
http://localhost:8080/index.html
```

### Fluxo Completo de Cadastro

#### Pessoa Física (CPF)
1. Acesse a página inicial
2. Clique em **"Quero me Cadastrar"**
3. Selecione **"Pessoa Física (CPF)"**
4. Preencha seus dados pessoais
5. Complete seu perfil de voluntário
6. Aceite o termo de compromisso
7. Copie o token gerado
8. Valide seu email com o token
9. Aguarde aprovação

#### Pessoa Jurídica (CNPJ)
1. Acesse a página inicial
2. Clique em **"Quero me Cadastrar"**
3. Selecione **"Pessoa Jurídica (CNPJ)"**
4. Preencha certidões
5. Informe dados do representante legal
6. Complete o perfil
7. Aceite o termo e valide o token

### Comandos Úteis

```bash
# Iniciar servidor
bash run.sh

# Parar servidor
pkill -f "java.*WebServer"

# Consultar banco de dados
mysql -u root -e "USE rede_mais_social; SELECT * FROM candidato;"

# Recompilar (se necessário)
javac -d bin -cp ".:mysql-connector-j-8.0.33.jar" src/*.java
```

---

## 📁 Estrutura do Projeto

```
Projeto-da-Rede-Mais-Social/
│
├── src/                          # Código-fonte Java
│   ├── WebServer.java            # Servidor HTTP
│   ├── AfiliacaoController.java  # Lógica de negócio
│   ├── Candidato.java            # Model - Candidato
│   ├── Afiliacao.java            # Model - Afiliação
│   ├── CandidatoDAO.java         # Acesso ao banco (candidatos)
│   ├── AfiliacaoDAO.java         # Acesso ao banco (afiliações)
│   ├── DatabaseConnection.java   # Configuração MySQL
│   ├── EmailService.java         # Envio de emails
│   └── Validador.java            # Validações
│
├── bin/                          # Classes compiladas
│
├── web/                          # Interface web
│   ├── index.html                # Página inicial
│   ├── tipo-afiliacao.html       # Escolha CPF/CNPJ
│   ├── formulario-identificacao.html
│   ├── formulario-cnpj.html
│   ├── formulario-representante-cnpj.html
│   ├── formulario-perfil.html
│   ├── termo-compromisso.html
│   ├── validacao-email.html
│   ├── login.html
│   ├── status-aguardando.html
│   └── styles.css                # Estilos CSS
│
├── mysql-connector-j-8.0.33.jar  # Driver JDBC
├── scriptBancoDados.txt          # Script SQL
├── run.sh                        # Script de execução
├── README.md                     # Este arquivo
├── INSTALACAO_MYSQL.txt          # Guia de instalação MySQL
├── INSTRUCOES_EXECUCAO.txt       # Instruções detalhadas
├── EXPLICACAO_CODIGO.txt         # Explicação do código
└── ROTEIRO_VIDEO.txt             # Roteiro de apresentação
```

---

## 🏗️ Arquitetura

O sistema segue o padrão **MVC (Model-View-Controller)**:

### Camadas

```
┌─────────────────────────────────────────────────┐
│              APRESENTAÇÃO (View)                │
│         HTML + CSS + JavaScript                 │
└─────────────────┬───────────────────────────────┘
                  │ HTTP/JSON
┌─────────────────▼───────────────────────────────┐
│           SERVIDOR (WebServer)                  │
│         Processa requisições HTTP               │
└─────────────────┬───────────────────────────────┘
                  │
┌─────────────────▼───────────────────────────────┐
│         CONTROLE (Controller)                   │
│    AfiliacaoController - Lógica de negócio     │
└─────────────────┬───────────────────────────────┘
                  │
┌─────────────────▼───────────────────────────────┐
│           ACESSO A DADOS (DAO)                  │
│    CandidatoDAO + AfiliacaoDAO                  │
└─────────────────┬───────────────────────────────┘
                  │ JDBC
┌─────────────────▼───────────────────────────────┐
│           BANCO DE DADOS (MySQL)                │
│    Tabelas: candidato, afiliacao                │
└─────────────────────────────────────────────────┘
```

### Fluxo de Dados

1. **Frontend** → Envia JSON via `fetch()`
2. **WebServer** → Recebe e roteia para handler adequado
3. **Controller** → Valida dados e aplica regras de negócio
4. **DAO** → Executa operações no banco de dados
5. **MySQL** → Armazena/retorna dados
6. **Backend** → Retorna JSON com resultado
7. **Frontend** → Exibe resposta ao usuário

---

## 📚 Documentação

### Documentação Detalhada

- **[INSTRUCOES_EXECUCAO.txt](INSTRUCOES_EXECUCAO.txt)** - Passo a passo completo para executar
- **[EXPLICACAO_CODIGO.txt](EXPLICACAO_CODIGO.txt)** - Explicação linha por linha do código
- **[ROTEIRO_VIDEO.txt](ROTEIRO_VIDEO.txt)** - Roteiro para apresentação em vídeo
- **[INSTALACAO_MYSQL.txt](INSTALACAO_MYSQL.txt)** - Guia de instalação e configuração MySQL

### Wiki do Projeto

A documentação técnica completa está disponível na Wiki:

- [Descrição do projeto e cenários](https://github.com/teterichard/Projeto-da-Rede-Mais-Social/wiki/1.-Descri%C3%A7%C3%A3o-do-projeto-e-cen%C3%A1rios)
- [Sequência de Telas - Cenário 1](https://github.com/teterichard/Projeto-da-Rede-Mais-Social/wiki/2.-Sequ%C3%AAncia-de-Telas--%E2%80%90-Cen%C3%A1rio-1)
- [Sequência de Telas - Cenário 2](https://github.com/teterichard/Projeto-da-Rede-Mais-Social/wiki/3.-Sequ%C3%AAncia-de-Telas-%E2%80%90-Cen%C3%A1rio-2)
- [Diagrama UML](https://github.com/teterichard/Projeto-da-Rede-Mais-Social/wiki/4.-Diagrama-UML)
- [Diagrama de Classes de Sequência](https://github.com/teterichard/Projeto-da-Rede-Mais-Social/wiki/5.-Diagrama-de-Classes-de-Sequ%C3%AAncia)
- [Modelo Entidade Relacionamento (MER)](https://github.com/teterichard/Projeto-da-Rede-Mais-Social/wiki/6.-Modelo-Entidade-Relacionamento-(MER))
- [Script Banco de Dados](https://github.com/teterichard/Projeto-da-Rede-Mais-Social/wiki/7.-Script-Banco-de-Dados)

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Faça um Fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/NovaFuncionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abra um Pull Request

---

## 📝 Licença

Este projeto foi desenvolvido para fins acadêmicos.

---

## 👥 Autores

Desenvolvido por estudantes de Engenharia de Software como projeto da disciplina.

---

## 📞 Suporte

Se você encontrou algum problema ou tem dúvidas:

1. Consulte os arquivos de documentação na pasta do projeto
2. Verifique a seção de [Issues](https://github.com/LeoMoreeiraa/Projeto-da-Rede-Mais-Social/issues)
3. Consulte o arquivo [INSTALACAO_MYSQL.txt](INSTALACAO_MYSQL.txt) para problemas com banco de dados

---

## 🎓 Aprendizados

Este projeto proporcionou experiência prática em:

- ✅ Desenvolvimento full-stack com Java
- ✅ Arquitetura MVC e padrões de projeto
- ✅ Integração com banco de dados MySQL
- ✅ Desenvolvimento de APIs REST
- ✅ Validações e segurança web
- ✅ Interface responsiva com HTML/CSS/JS
- ✅ Gestão de sessões com sessionStorage
- ✅ Trabalho em equipe e versionamento Git

---

<p align="center">
  Feito com ❤️ para conectar pessoas que querem fazer a diferença
</p>
