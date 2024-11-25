
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


## Endpoints Disponíveis 📑

### Products (Produtos):

~~~javascript
Listar todos os produtos: GET /products
Detalhes de um produto específico: GET /products/:id
~~~

Caso nao consiga gerar use a key abaixo: 
~~~javascript
Api token reserva: 53ab0c2f8f03fc339ca7963fba5534433c4ee17136fe86cf7e0884b0891d3c6e27ee8c2b16ed0376f656306b6bb4a4f643ad6d344079cd8008a0fc071bb5a6c2ebf3bd51a93228c57983e12c26591b7e0e5b7bd42ec1b82506f49332871fde6370d4ecbe07bdc62cafa1555dec265adec77eb1affc29e4c854b2d915c228300b
~~~



## 📡 Consumindo a API com JS:

Este guia mostra como consumir uma API RESTful com JavaScript, utilizando fetch() para fazer requisições e manipular o DOM. O exemplo foca em consumir dados de uma API Strapi e exibi-los em uma página web.

### O que é JSON?
JSON (JavaScript Object Notation) é um formato de dados leve e fácil de ler e escrever, amplamente utilizado para trocar informações entre cliente e servidor. No JavaScript, você pode transformar a resposta JSON em um objeto utilizável com o método `.json()`.

1. Defina a URL da API e o Token:

Comece definindo a URL da API que você deseja consumir e o token de autorização que será necessário nas requisições.

~~~javascript
const apiUrl = 'https://ecom-back-strapi.onrender.com/api/products';
const token = 'Bearer SEU_TOKEN_AQUI'; // Insira seu token aqui
~~~

2. Crie uma Função para Configurar os Cabeçalhos:

Crie uma função que retorna os cabeçalhos necessários para a requisição, incluindo o token de autorização.
~~~javascript
function configurarCabecalhos() {
    return {
        'Authorization': token,
        'Content-Type': 'application/json'
    };
}
~~~

3. Faça a Requisição à API:

Use a função fetch para fazer uma requisição GET à API dentro de uma função assíncrona. Verifique a resposta e trate os erros adequadamente.

~~~javascript
async function buscarProdutos() {
    try {
        const response = await fetch(apiUrl, {
            method: 'GET',
            headers: configurarCabecalhos()
        });

        if (!response.ok) {
            throw new Error('Erro na resposta da API: ' + response.status);
        }

        const data = await response.json();
        return data.data; // Retorna os produtos
    } catch (error) {
        console.error('Erro ao buscar dados da API:', error);
        return null; // Em caso de erro
    }
}
~~~

4. Exiba os Produtos:

Crie uma função que aceita os produtos como parâmetro e cria elementos HTML para cada um deles, exibindo as informações na página.

~~~javascript
function exibirProdutos(produtos) {
    const produtosContainer = document.getElementById('produtos');
    produtosContainer.innerHTML = ''; // Limpa o container antes de adicionar novos produtos

    produtos.forEach(produto => {
        // Crie um elemento de produto
        const produtoDiv = document.createElement('div');
        produtoDiv.classList.add('produto');

        // Adicione a imagem do produto
        const imagem = document.createElement('img');
        imagem.src = produto.imagens[0]; // Usa a primeira imagem
        imagem.alt = produto.nome;
        imagem.classList.add('produto-imagem');

        // Adicione o nome e preço do produto
        const nome = document.createElement('h2');
        nome.textContent = produto.nome;

        const preco = document.createElement('p');
        preco.textContent = `Preço: R$ ${produto.preco.toFixed(2)}`;

        // Adicione um botão de compra
        const botaoComprar = document.createElement('button');
        botaoComprar.textContent = 'Comprar';
        botaoComprar.onclick = () => {
            // Aqui você pode adicionar lógica para o botão de compra
            alert(`Você comprou: ${produto.nome}`);
        };

        // Adicione os elementos ao container do produto
        produtoDiv.appendChild(imagem);
        produtoDiv.appendChild(nome);
        produtoDiv.appendChild(preco);
        produtoDiv.appendChild(botaoComprar);
        produtosContainer.appendChild(produtoDiv);
    });
}

~~~

5. Função Principal para Executar o Fluxo:

Por fim, crie uma função principal que chama as funções de buscar produtos e exibir produtos.

~~~javascript
async function iniciarApp() {
    const produtos = await buscarProdutos();
    if (produtos) {
        exibirProdutos(produtos);
    } else {
        console.error('Nenhum produto encontrado.');
    }
}

// Chame a função principal ao carregar a página
window.onload = iniciarApp;

~~~

## **Boa sorte e bom código!** 🚀📘

