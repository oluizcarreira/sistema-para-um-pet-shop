# 🐾 Sistema de Gerenciamento para Pet Shop

Este projeto consiste em um sistema CRUD completo para gerenciamento de um Pet Shop, desenvolvido como trabalho acadêmico para a disciplina de **Banco de Dados NoSQL**. A aplicação foca na flexibilidade de esquemas oferecida pelo MongoDB integrada a uma interface web dinâmica e segura.

---

## 🛠️ Tecnologias Utilizadas

* **Backend:** Python 3.x com Flask (Microframework)
* **Banco de Dados:** MongoDB (Banco orientado a documentos)
* **Driver de Conexão:** PyMongo
* **Segurança:** Werkzeug (criptografia Hash para senhas) e `python-dotenv` para variáveis de ambiente.
* **Frontend:** HTML5, CSS3, Jinja2 Templates e Bootstrap (componentes de alertas e formulários).

---

## 🔬 Diferenciais de Arquitetura e NoSQL

Por se tratar de um projeto com foco em banco de dados NoSQL (Documentos), a aplicação explora as seguintes características essenciais:

* **Esquema Dinâmico (Schema-less):** Armazenamento de dados complexos dos pets e clientes em documentos JSON-like únicos dentro do MongoDB, facilitando a expansão futura de campos sem a necessidade de migrações complexas estruturais (SQL).
* **Agregação de Dados:** Campos como `cadastrado_por_id` e `cadastrado_por_username` são injetados diretamente no documento do pet na criação (`insert_one`), eliminando a necessidade de JOINS complexos durante a listagem dos dados.
* **Queries Avançadas com PyMongo:** Utilização de operadores de busca complexos, como expressões regulares (`$regex` com `$options: 'i'`), filtros por intervalo de datas (`$gte`, `$lte`), operadores lógicos (`$and`, `$or`) e ordenação dinâmica em nível de banco de dados (`ASCENDING` / `DESCENDING`).

---

## 🔒 Camada de Segurança Integrada

* **Autenticação Obrigatória:** Sistema protegido por sessão (`session`). Rotas críticas do CRUD utilizam um decorator personalizado `@login_required` para impedir acessos não autorizados por URL direta.
* **Segurança de Senhas:** O banco de dados **nunca** armazena senhas em texto puro. Utiliza o método `generate_password_hash` da biblioteca Werkzeug (com algoritmos robustos de hash e salt) no cadastro, validando os acessos via `check_password_hash`.
* **Tratamento de Exceções Baseado em Objetos:** Proteção contra quebras na aplicação ao validar dinamicamente as strings de ID em instâncias de `ObjectId(id)`.
* **Zero Hardcoded Credentials:** Todas as credenciais de banco, portas e chaves de criptografia da aplicação ficam isoladas em um arquivo ambiente privado (`.env`).

---

## 📂 Estrutura do Projeto

```text
.
├── static/
│   ├── background.jpg
│   ├── logo.png
│   └── style.css
├── templates/
│   ├── base.html       # Estrutura base da página (Navbar, mensagens Flash)
│   ├── welcome.html    # Tela de boas-vindas inicial
│   ├── login.html      # Tela de login
│   ├── register.html   # Tela de cadastro de usuários
│   ├── list.html       # Painel principal (Listagem com filtros de busca)
│   ├── detail.html     # Exibição detalhada do Pet/Dono
│   ├── create.html     # Formulário de inserção de pets
│   └── edit.html       # Formulário de edição de dados
├── .gitignore
├── LICENSE
├── app.py              # Código principal e gerenciamento das rotas
└── requirements.txt    # Dependências do projeto
⚙️ Como Executar o Projeto Localmente
1. Clonar o repositório
Bash
git clone [https://github.com/seu-usuario/sistema-para-um-pet-shop.git](https://github.com/seu-usuario/sistema-para-um-pet-shop.git)
cd sistema-para-um-pet-shop
2. Configurar o Ambiente Virtual (Opcional, mas recomendado)
Bash
python -m venv venv
source venv/bin/activate  # No Linux/Mac
# venv\Scripts\activate   # No Windows
3. Instalar as dependências
Bash
pip install -r requirements.txt
4. Configurar as Variáveis de Ambiente
Crie um arquivo .env na raiz do projeto com as seguintes chaves preenchidas:

Snippet de código
SECRET_KEY="sua_chave_secreta_flask"
DATABASE_URL="sua_string_de_conexao_mongodb"
DB="nome_do_seu_banco_de_dados"
COLPET="nome_da_sua_collection_de_pets"
COLUSR="nome_da_sua_collection_de_usuarios"
5. Executar a aplicação
Bash
python app.py
Acesse http://127.0.0.1:5000/ no seu navegador.
