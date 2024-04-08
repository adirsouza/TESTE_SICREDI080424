# Desafio Técnico de QE para o Sicredi

Este documento fornece uma visão geral do Desafio Técnico de Engenharia da Qualidade (QE) proposto pelo Sicredi. Ele inclui detalhes sobre o projeto, instruções de execução, plano de teste, estratégias de testes, bugs identificados durante os testes e possíveis melhorias.

## 1. Informações do Projeto
Esse teste tem como objetivo realizar o teste automatizado das Api´s informadas, bem como a Documentação que compõe o processo de teste como: entendimento, plano e cenários de testes, implementação de testes automatizados, Relatório e conclusão.
Tecnologias utilizadas: Java, Maven, Unirest, Junit e Intellij
Descreva aqui o objetivo do projeto, tecnologias utilizadas, estrutura do projeto e quaisquer outras informações relevantes que ajudem a entender o contexto e os objetivos do desafio.

## 2. Como Executar

Forneça um guia passo a passo sobre como configurar e executar o projeto localmente. Isso pode incluir:

##### 2.1 Pré-requisitos:
- Java jdk 21;
- Maven;
- Unirest;
- Junit ;
- Intellij.

##### 2.2 Configuração do ambiente:
- Clone o projeto do GitLab localmente;
- Instale o Intelji ;
  a.	Acesse o site https://www.jetbrains.com/pt-br/idea/ ;
  b. 	Vá em baixar e clique em baixar (de preferencia a versão Intelji ultimate);
  c.	Execute o setup .exe;
  d. 	Em instaletion Options marque os campos(Add folden as Project, java);
  e. 	Clique em instalar.

- Preparando o InelJI
  a. Abra o intelJI ;
  b. Selecione a opção open;
  c. Selecione a pasta do projeto que você clonou;
  d. Espere o intelJI instalar as dependências;

- Caso o Intelij não baixe automaticamente
  a.	Com o Projeto aberto;
  b.	Clique no Arquivo “pom” para abrir;
  c.	No código do arquivo “pom” clique com o botão direito e clique em “Download
  Sources” para baixar as Dependências do projeto;
  d. No menu superior (representado pelas 4 barras);
  e. Vá em “Project Structure”;
  f. Em “SDK” clique e selecione “dowload sdk”;
  g. Depois em “Apply” no canto inferior direito;
  h. Espere a IDE baixar o SDK 21.

##### 2.3 Executando os testes
- Navegue até a pasta “Teste” pelo caminho: TesteSicredi>src>main>java>com.desafio.sicredi>Teste;
- Clique com o botão direito em cima da pasta “Teste” e Clique na opçaõ de “Run”.

##### 2.4	Geração de Relatório
- Após realizar o teste ;
- No terminal, clicar em more (representado pelos três pontos);
- Selecionar Exportar os resutados dos testes;
- Selecionar o formato de HTML de preferência;
- Marque a opção "Open exported file in browser";
- Confirmar em Ok;
- O Relatorio irá abrir no browser.

## 3. Plano de Teste e Estratégia de Testes

### Objetivo dos Testes:
Assegurar que as APIs funcionem conforme esperado em diferentes cenários, incluindo sucesso, falha e uso anormal. Além disso, garantir a segurança e a eficiência no manuseio de dados sensíveis como credenciais de usuário.

### Estratégias de Teste:
1. **Testes Funcionais**: Validar a funcionalidade de cada endpoint, garantindo que eles atendam aos requisitos especificados.
2. **Testes de Validação**: Verificar se os campos de entrada são validados corretamente pela API, incluindo testes de campos obrigatórios e formatos de dados esperados.
4. **Testes de Integração**: Verificar como os diferentes endpoints interagem entre si, especialmente a sequência de autenticação e acesso a recursos protegidos.

### Cenários de Teste

#### 1. TesteBuscarStatusAplicação
Para a API `GET/test` que verifica o status da aplicação, um plano de teste deve cobrir verificações básicas para assegurar que a API esteja acessível e respondendo conforme esperado.
### Cenários de Teste Positivos

1. **Verificar Status da Aplicação**:
    - Enviar uma requisição GET para o endpoint `/test`.
    - Verificar se a resposta é `200 OK` e se o corpo da resposta contém o JSON esperado com os campos `status` e `method`, onde `status` deve ser `"ok"` e `method` deve indicar `"GET"`.

### Cenários de Teste Negativos

2. **Uso de Método HTTP Incorreto**:
    - Tentar acessar o endpoint `/test` com um método HTTP diferente de GET, como POST, PUT, DELETE, etc.
    - Verificar se a resposta é um código de erro apropriado, como `405 Method Not Allowed`, e se há uma mensagem indicando que o método utilizado não é suportado.

3. **Endpoint Inexistente**:
    - Enviar uma requisição para um endpoint inexistente ou digitado incorretamente, por exemplo, `/testInvalido`.
    - Verificar se a resposta é `404 Not Found` e se há uma mensagem indicando que o endpoint não foi encontrado.

#### 2. TesteBuscarVerificarDadosUsuarios

Para a API `GET/users` que verifica o status da aplicação, um plano de teste deve cobrir verificações básicas para assegurar que a API esteja acessível e respondendo conforme esperado.
### Cenários de Teste Positivos:

1. **Validação de Campos Importantes**:
    - Focar nos campos `username` e `password`, pois são críticos para o processo de autenticação.
    - Verificar se cada usuário na lista inclui esses campos e se os valores parecem válidos e consistentes.

2. **Filtragem e Busca por id validos**:
    - Verificar se é possivel buscar um usuario pelo id.
    - Verificar se a resposta é adequada, como `200 OK`.

### Cenários de Teste Negativos

3. **Filtragem e Busca por Id  inválidos**:
    - Se a API suportar filtragem ou busca por parâmetros específicos (como `id`), testar com valores inválidos.
    - Verificar se a resposta é adequada, como `200 OK` com uma lista vazia ou `404 Not Found`, dependendo da implementação da API.

### Cenários de Teste de Validação de Dados

4. **Integridade e Formatação dos Dados**:
    - Verificar a integridade e formatação dos dados retornados, garantindo que todos os campos estejam presentes e corretos, especialmente os campos importantes para a autenticação.
    - Confirmar que os campos de dados pessoais e de contato, como `email` e `phone`, seguem os formatos padrão.

5. **Validação de campos importantes**:
    - Verificar a integridade e formatação dos dados retornados, garantindo que todos os campos estejam presentes e corretos, especialmente os campos importantes para a autenticação.
    - Confirmar que os campos de dados pessoais e de contato, como `email` e `phone`, seguem os formatos padrão.

#### 3. TesteValidaçãoLogin

Para a API `POST/auth/login` que realiza a criação de token para autenticação, um plano de teste deve abranger a validação do processo de login, a geração correta do token e o tratamento de erros. Aqui estão os cenários de teste sugeridos:

### Cenários de Teste Positivos

1. **Login com Credenciais Válidas**:
    - Enviar uma requisição com um `username` e `password` válidos.
    - Verificar se a resposta é `201 OK` e se o corpo da resposta contém o `token` de autenticação, juntamente com detalhes do usuário como `id`, `username`, `email`, `firstName`, `lastName`, `gender`, `image`.

2. **Validade do Token**:
    - Usar o token de autenticação fornecido na resposta para acessar outros endpoints protegidos e verificar se o token é aceito e válido.

### Cenários de Teste Negativos

3. **Login com Credenciais Inválidas**:
    - Enviar uma requisição com `username` ou `password` incorretos.
    - Verificar se a resposta é um código de erro adequado, como `401 Unauthorized`, e se há uma mensagem indicando que as credenciais são inválidas.

4. **Campos ausentes na Requisição**:
    - Enviar uma requisição sem `username` ou `password`.
    - Verificar se a resposta é `400 Bad Request` e se há uma mensagem indicando que os campos necessários estão faltando.


#### 4. TesteBuscarProdutosAutenticação

Para a API `GET/auth/products` que verifica o status da aplicação, um plano de teste deve cobrir verificações básicas para assegurar que a API esteja acessível e respondendo conforme esperado.

### Cenários de Teste Positivos

1. **Acesso com Token Válido**:
    - Usar um token de autenticação válido no cabeçalho da requisição.
    - Verificar se a resposta é `200 OK` e se a lista de produtos é retornada corretamente.

### Cenários de Teste Negativos

2. **Token autenticação  ausente**:
    - Enviar uma requisição sem o cabeçalho de autenticação.
    - Verificar se a resposta é `401 Unauthorized` e contém uma mensagem de erro indicando a falta do token.

3. **Token de Autenticação Inválido**:
    - Usar um token inválido ou expirado no cabeçalho de autenticação.
    - Verificar se a resposta é `401 Unauthorized` ou `403 Forbidden` e contém uma mensagem de erro adequada.

### Cenários de Teste de Validação de Dados

4. **Estrutura dos Dados dos Produtos**:
    - Verificar se a estrutura dos dados dos produtos na resposta corresponde ao esperado, incluindo todos os campos obrigatórios como `id`, `title`, `price`, `brand`, `category`, `thumbnail`, etc.

#### 5. TesteCriaçãoProdutos

Para a API `POST/products/add` que verifica o status da aplicação, um plano de teste deve cobrir verificações básicas para assegurar que a API esteja acessível e respondendo conforme esperado.

### Cenários de Teste Positivos

1. **Criação de Produto com Todos os Campos**:
    - Enviar uma requisição com todos os campos preenchidos corretamente.
    - Verificar se a resposta é `201 OK`

### Cenários de Teste Negativos

2. **Criação de Produto Sem Body**:
    - Enviar um body vazio
    - Verificar se a resposta  `400 Bad Request` e se há mensagens de erro específicas para os campos inválidos.

3. **Criar Produto Com Tipos De Dados Inválidos**:
    - Enviar uma requisição com valores inválidos para campos específicos (Onde for String passar INT e vice versa).
    - Verificar se a resposta é `400 Bad Request` e se há mensagens de erro específicas para os campos inválidos.

### Cenários de Teste de Integração

4. **Visualização Após Criação**:
    - Após criar um produto, tentar visualizá-lo usando um endpoint adequado (se disponível) para garantir que foi criado corretamente.
    - Nota: Isso pode não ser aplicável pois os produtos criados não são persistentes, conforme a nota fornecida.

#### 6. Teste Buscar todos os produtos

Para a API `GET/productS` que verifica o status da aplicação, um plano de teste deve cobrir verificações básicas para assegurar que a API esteja acessível e respondendo conforme esperado.

### Cenários de Teste Positivos

1. **Buscar Todos Produtos Listados**:
    - Enviar uma requisição para buscar todos os produtos da lista.
    - Verificar se a resposta é `200 OK` e se a lista de produtos é retornada conforme esperado.

### Cenários de Teste de Validação de Dados

2. **Validação dos Dados dos Produtos**:
    - Verificar se os dados de cada produto na lista estão completos e corretos, conferindo o detalhe do preço.

3. **Verificar Total De Produtos**:
    - Verifica se o total de produtos listado no response E igual há 100

#### 7. TesteBuscarProdutoPorID

### Cenários de Teste Positivos

Para a API `GET/products/{id}` que verifica o status da aplicação, um plano de teste deve cobrir verificações básicas para assegurar que a API esteja acessível e respondendo conforme esperado.

1. **Produto Com Id Valido**:
    - Enviar uma requisição com um ID de produto válido.
    - Verificar se a resposta é `200 OK` e se os dados do produto retornado correspondem ao ID solicitado.

### Cenários de Teste Negativos

2. **Produto Com Id Inexistente**:
    - Enviar uma requisição com um ID de produto que não existe 999999.
    - Verificar se a resposta é `404 Not Found` e se a mensagem de erro informa que o produto não foi encontrado.

3. **ID de Produto Inválido**:
    - Enviar uma requisição com um ID de produto inválido "teste".
    - Verificar se a resposta é `404 Not Found`, e se há uma mensagem de erro adequada..

### Resumo dos Testes automatizados
Dado os Cenários de testes planejados, foi realizado um total de 26 Testes, onde 22 de Sucesso e 4 de Falha.
Os testes da falha estão abordados no tópico de Bugs.

### Conclusão
Este plano abrange uma abordagem abrangente para testar as APIs fornecidas, focando na funcionalidade e segurança. A implementação deste plano ajudará a garantir que a API atenda aos requisitos de negócios e técnicos, mantendo os dados dos usuários seguros e otimizando a experiência do usuário.

## 4. Bugs

•**Uso de Método HTTP Incorreto**:
- Tentar acessar o endpoint `/test` com um método HTTP diferente de GET, como POST, PUT, DELETE, etc.
- Verificar se a resposta é um código de erro apropriado, como `405 Method Not Allowed`, e se há uma mensagem indicando que o método utilizado não é suportado.
  Nesse cenário a resposta do status code foi 200 de sucesso, que segundo a documentação só deveria ser permitido o methodo GET

•   **Criação de Produto com Campos Obrigatórios**:
- Verificar se a resposta é `201 OK` e se o produto é criado com valores padrão.
  Nesse caso a resposta do status code foi 200 de sucesso, porém segundo a Documentação o staus code deve ser 201, como o padrão da API rest solicita.


•  **Criação de Produto com Campos Ausentes **:
-Quando tenta criar um produto com campos ausentes e o produto é criado da mesma
Deveria retornar um erro ao tentar criar um produto com dados ausentes.

•  **Criação de Produto com Campos Inválidos**:
-Quando tenta criar um produto com campos ausentes e o produto é criado da mesma
Deveria retornar um erro ao tentar criar um produto com dados inválidos.


Para mais informações, entre em contato com William de Souza Pereira
E-mail : souzatechconsult@gmail.com
Telefone WhatsApp: +55 (41|) 995153282
