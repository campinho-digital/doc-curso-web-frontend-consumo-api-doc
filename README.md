## O que é uma API?

Uma API (Application Programming Interface) é um conjunto de definições e protocolos que permitem que diferentes sistemas se comuniquem. No contexto de aplicações web, uma API geralmente expõe endpoints que permitem que desenvolvedores interajam com um servidor para realizar ações como obter dados, enviar informações, atualizar registros, ou deletar recursos. A API utiliza formatos padronizados, como JSON, para que os dados sejam facilmente compreendidos.

### O que é JSON?

JSON (JavaScript Object Notation) é um formato de dados leve, fácil de ler e escrever, amplamente utilizado para troca de informações entre cliente e servidor. É baseado na sintaxe de objetos do JavaScript, mas pode ser usado em praticamente qualquer linguagem de programação. No JSON, os dados são organizados em pares de chave-valor:

~~~json
{
  "id": 1,
  "name": "Produto A",
  "price": 29.99,
  "inStock": true
}

~~~

- Chave (key): Nome que identifica o dado. Ex: "name", "price".
- Valor (value): O dado correspondente. Ex: "Produto A", 29.99.


## 📡 Testando a Api no Postman:

Ao testar a Api utilizando o postman podemos validar o formato e estrutura: ver como os dados chegam da API permite que o desenvolvedor entenda o formato (JSON, XML, etc.), a estrutura dos objetos, os campos disponíveis e seus tipos. Isso ajuda a planejar como manipular e renderizar esses dados no front-end.

#### ⚠️ Atenção  Se a API exigir uma chave de autenticação (API Key) e você tentar fazer uma requisição sem ela, receberá um erro de resposta, geralmente com um código de status 401 (Não autorizado).

Exemplo do postman sem `API KEY`

<img width="1027" alt="Captura de Tela 2024-11-04 às 10 53 38" src="https://github.com/user-attachments/assets/43bbacb7-88b3-407a-843b-fafbd26477ee">

### Conseguindo sua API Key 

Será nencessário um *POST* usando as seguintes credenciais para conseguir a sua A `Api key`

~~~json
https://ecom-back-strapi.onrender.com/api/auth/local
~~~


~~~json
{
  "identifier": "campinho@mail.com",
  "password": "Campinho@12"
}
~~~

Você deve enviar um corpo JSON com as credenciais do usuário acima. Como na foto abaixo:

<img width="1057" alt="Captura de Tela 2024-11-04 às 12 52 41" src="https://github.com/user-attachments/assets/22cafe06-d843-4936-aee4-e4b1cb0bfcae">


a resposta da sua requisição tera um `JWT` que vc deverá usar como `API KEY` 
~~~json
{
    "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNzMwNzM1NTUzLCJleHAiOjE3MzMzMjc1NTN9.8tahgsa-twuEcgyDvmwl2R9QCHRlEsppSl95FmpKcBA",
    "user": {
        "id": 1,
        "username": "campinho",
        "email": "campinho@mail.com",
        "provider": "local",
        "confirmed": false,
        "blocked": false,
        "createdAt": "2024-11-04T15:49:10.569Z",
        "updatedAt": "2024-11-04T15:49:10.569Z"
    }
}
~~~


### Certifique-se de incluir a API Key no cabeçalho da requisição da seguinte forma:

~~~javascript
Authorization: Bearer SUACHAVE
~~~

<img width="1029" alt="Captura de Tela 2024-11-04 às 13 09 02" src="https://github.com/user-attachments/assets/e447f9ce-f942-457b-a56d-171d641f010c">



Caso nao consiga gerar use a key abaixo: 
~~~javascript
Api token reserva: 53ab0c2f8f03fc339ca7963fba5534433c4ee17136fe86cf7e0884b0891d3c6e27ee8c2b16ed0376f656306b6bb4a4f643ad6d344079cd8008a0fc071bb5a6c2ebf3bd51a93228c57983e12c26591b7e0e5b7bd42ec1b82506f49332871fde6370d4ecbe07bdc62cafa1555dec265adec77eb1affc29e4c854b2d915c228300b
~~~

## Endpoints Disponíveis 📑

### Products (Produtos):

~~~javascript
Listar todos os produtos: GET /products
Detalhes de um produto específico: GET /products/:id
~~~


### Movies (Filmes):

~~~javascript
Listar todos os produtos: GET /movies
Detalhes de um produto específico: GET /movies/:id
~~~


### Animes:

~~~javascript
Listar todos os animes: GET /animes
Detalhes de um anime específico: GET /animes/:id
~~~


### Livros:

~~~javascript
Listar todos os livros: GET /books
Detalhes de um livro específico: GET /books/:id
~~~


### Futebol:

~~~javascript
Listar todos os times: GET /futebol
Detalhes de um time específico: GET /futebol/:id
~~~

### Games:

~~~javascript
Listar todos os jogos: GET /games
Detalhes de um jogo específico: GET /games/:id
~~~


## **Boa sorte e bom código!** 🚀📘

