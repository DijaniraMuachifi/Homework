# Homework
# Tutorial: Criação de uma API da Web com ASP.NET Core

### Última atualização: 23/08/2024  
**Autores:** Rick Anderson e Kirk Larkin

Este repositório é um guia passo a passo para criar uma API da Web utilizando **ASP.NET Core** com um banco de dados de apoio, focado em APIs baseadas em controladores. Para aqueles interessados em APIs mínimas, consulte o [Tutorial: Crie uma API mínima com o ASP.NET Core](link para o tutorial de API mínima).

### Estrutura do Tutorial

1. **Visão Geral**:  
   Este tutorial cobre a criação de uma API com as seguintes rotas:

   - `GET /api/todoitems`: Retorna todos os itens de tarefas
   - `GET /api/todoitems/{id}`: Retorna um item específico
   - `POST /api/todoitems`: Adiciona um novo item
   - `PUT /api/todoitems/{id}`: Atualiza um item existente
   - `DELETE /api/todoitems/{id}`: Exclui um item

   Um diagrama descreve a arquitetura do app, demonstrando o fluxo entre cliente, controlador, modelo e camada de dados.

2. **Pré-requisitos**:
   - Visual Studio ou Visual Studio Code (com o suporte para desenvolvimento ASP.NET e web)
   - Familiaridade com ASP.NET Core e Entity Framework Core

3. **Passos Detalhados do Projeto**:
   - **Criação do Projeto Web**: Inicie um projeto ASP.NET Core Web API no Visual Studio.
   - **Adicionar Pacotes NuGet**: Use o `Microsoft.EntityFrameworkCore.InMemory` para suportar um banco de dados em memória, ideal para testes e desenvolvimento inicial.
   - **Testar o Projeto**: O projeto inclui uma API `WeatherForecast` para testes iniciais, acessível via Swagger.

4. **Estrutura de Código**:
   - **Classe de Modelo (`TodoItem`)**: A classe `TodoItem` representa a estrutura de um item de tarefa.
   - **Contexto de Banco de Dados (`TodoContext`)**: Responsável por gerenciar o acesso ao banco de dados.
   - **Configuração do `Program.cs`**: Registra o contexto do banco de dados e configura o Swagger para documentação automática da API.

5. **Implementação do Controlador**:  
   - Scaffold do controlador da API para incluir operações CRUD usando Entity Framework.
   - **Método `PostTodoItem`**: Modificado para retornar um cabeçalho `Location` com o URI do novo item criado.

6. **Teste da API com Swagger**:
   - Acesse `POST /api/TodoItems` para adicionar itens e `GET /api/TodoItems/{id}` para consultá-los.
   - Os testes incluem verificações dos códigos de resposta HTTP, como o 201 para criação bem-sucedida.

7. **Mais Informações**:
   - Para uma visão geral sobre ASP.NET Core com Swagger e OpenAPI, consulte [Documentação ASP.NET Core](link para a documentação).
  

### 1. **Pré-requisitos**
   - Ter o MongoDB 6.0.5 ou superior instalado.
   - Instalar o MongoDB Shell e configurar o acesso a partir da linha de comando.
   - Ferramentas de desenvolvimento, como Visual Studio ou VS Code.

### 2. **Configuração do MongoDB**
   - Configurar o MongoDB para acesso local.
   - Criar um banco de dados `BookStore` e uma coleção `Books`.
   - Inserir dados de exemplo na coleção para testes iniciais.

### 3. **Criação do Projeto API com ASP.NET Core**
   - No Visual Studio, criar um novo projeto do tipo **ASP.NET Core Web API** e selecionar a estrutura .NET 8.0.
   - Instalar o pacote `MongoDB.Driver` para conectar-se ao MongoDB.

### 4. **Definir o Modelo de Entidade**
   - Criar um modelo `Book` em um novo diretório `Models`, com atributos específicos para MongoDB, como `BsonId` para a chave primária e `BsonElement` para personalizar os nomes das propriedades.

### 5. **Adicionar Configurações de Banco de Dados**
   - Definir as configurações do banco de dados em `appsettings.json`, incluindo a string de conexão e o nome do banco e da coleção.
   - Criar uma classe `BookStoreDatabaseSettings` para mapear as configurações e facilitar o uso do Dependency Injection (DI) para acessar essas configurações.

### 6. **Serviço de Operações CRUD**
   - Criar a classe `BooksService` em um diretório `Services` para centralizar as operações de banco de dados. Essa classe implementa métodos para:
     - **GetAsync**: Retorna todos os documentos.
     - **GetAsync(id)**: Retorna um documento específico pelo ID.
     - **CreateAsync**: Insere um novo documento.
     - **UpdateAsync**: Atualiza um documento existente.
     - **RemoveAsync**: Remove um documento pelo ID.
   - Configurar o `BooksService` no contêiner de DI como singleton.

### 7. **Controlador da API (BooksController)**
   - Implementar um controlador `BooksController` no diretório `Controllers`.
   - Criar endpoints para atender aos métodos HTTP **GET**, **POST**, **PUT** e **DELETE**:
     - **GET /api/books**: Lista todos os livros.
     - **GET /api/books/{id}**: Retorna um livro específico.
     - **POST /api/books**: Adiciona um novo livro.
     - **PUT /api/books/{id}**: Atualiza um livro.
     - **DELETE /api/books/{id}**: Remove um livro.

### 8. **Testar a API**
   - Executar a API e testar os endpoints usando o navegador ou ferramentas como o Swagger.

### 9. **Configuração de Serialização JSON**
   - Ajustar a serialização JSON no `Program.cs` para que os nomes das propriedades no JSON sigam o formato Pascal Case, e modificar o nome da propriedade `BookName` para `Name`, aplicando `[JsonPropertyName("Name")]` na propriedade `BookName`.



### Principais etapas abordadas:

1. **Configuração do Projeto ASP.NET Core**: 
   - Inicia a configuração do `Program.cs` para habilitar o serviço de arquivos estáticos e a base de dados em memória (usando Entity Framework com `InMemoryDatabase`).
   - Inclui o uso de `DefaultFiles` e `StaticFiles` para permitir o uso de uma página HTML como ponto de entrada da aplicação.

2. **Estrutura de Diretórios**:
   - Criação de uma pasta `wwwroot` para armazenar arquivos estáticos, onde são criadas subpastas para `css` e `js`, além do arquivo HTML `index.html`.

3. **HTML (index.html)**:
   - Página HTML configurada para adicionar, editar e listar tarefas.
   - Formulários para adicionar novas tarefas e editar tarefas existentes.
   - Exibição de uma tabela dinâmica para listar os itens de tarefas com botões de `Editar` e `Excluir`.

4. **CSS (site.css)**:
   - Estilos básicos para exibir a tabela de tarefas e ajustar o layout dos formulários e botões.

5. **JavaScript (site.js)**:
   - Definição das funções CRUD utilizando `fetch` para interagir com a API:
     - **GetItems**: Envia uma requisição GET para listar todas as tarefas.
     - **AddItem**: Envia uma requisição POST para adicionar uma nova tarefa.
     - **UpdateItem**: Envia uma requisição PUT para atualizar uma tarefa existente.
     - **DeleteItem**: Envia uma requisição DELETE para excluir uma tarefa.

### Explicação dos Métodos CRUD:
- **Leitura de Tarefas**: `fetch(uri)` realiza a busca dos itens e atualiza a página HTML chamando a função `_displayItems`.
- **Adição de Tarefas**: Cria um objeto `item`, o converte em JSON, e o envia ao endpoint com método POST.
- **Atualização de Tarefas**: Similar à adição, mas com um endpoint específico para o ID do item e usando o método PUT.
- **Exclusão de Tarefas**: Configura o método DELETE para remover o item pelo seu ID.





 
