# CRUD-de-Produtos
Desafio 2 da matéria pin projeto em programação back end
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CRUD de Produtos</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f2f5;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }
        h1 {
            color: #333;
        }
        #menu {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 20px;
        }
        #menu button {
            margin: 5px 0;
            padding: 10px 20px;
            border: none;
            background-color: #4CAF50;
            color: white;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
        }
        #menu button:hover {
            background-color: #45a049;
        }
        table {
            width: 80%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        table, th, td {
            border: 1px solid #ddd;
        }
        th, td {
            padding: 10px;
            text-align: center;
        }
        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>
    <h1>CRUD de Produtos</h1>
    <div id="menu">
        <button onclick="mainMenu(1)">1 - Cadastrar produto</button>
        <button onclick="mainMenu(2)">2 - Editar produto</button>
        <button onclick="mainMenu(3)">3 - Deletar produto</button>
        <button onclick="mainMenu(4)">4 - Visualizar lista de produtos</button>
        <button onclick="mainMenu(0)">0 - Sair do sistema</button>
    </div>
    <div id="output"></div>
    
    <script src="script.js"></script>
</body>
</html>
let produtos = [];

function mainMenu(option) {
    switch (option) {
        case 0:
            alert("Saindo do sistema...");
            break;
        case 1:
            cadastrarProduto();
            break;
        case 2:
            editarProduto();
            break;
        case 3:
            deletarProduto();
            break;
        case 4:
            visualizarProdutos();
            break;
        default:
            alert("Opção inválida!");
            break;
    }
}

function cadastrarProduto() {
    let id = produtos.length ? produtos[produtos.length - 1].id + 1 : 1;
    let nome = prompt("Digite o nome do produto:");
    let quantidade = parseInt(prompt("Digite a quantidade do produto:"));
    let valor = parseFloat(prompt("Digite o valor do produto:"));
    let dataCadastro = new Date().toLocaleString();

    let produto = {
        id,
        nome,
        quantidade,
        valor,
        dataCadastro
    };

    produtos.push(produto);
    alert("Produto cadastrado com sucesso!");
}

function editarProduto() {
    let id = parseInt(prompt("Digite o ID do produto a ser editado:"));
    let produto = produtos.find(p => p.id === id);

    if (produto) {
        produto.nome = prompt("Digite o novo nome do produto:", produto.nome);
        produto.quantidade = parseInt(prompt("Digite a nova quantidade do produto:", produto.quantidade));
        produto.valor = parseFloat(prompt("Digite o novo valor do produto:", produto.valor));
        produto.dataCadastro = new Date().toLocaleString();

        alert("Produto editado com sucesso!");
    } else {
        alert("Produto não encontrado!");
    }
}

function deletarProduto() {
    let id = parseInt(prompt("Digite o ID do produto a ser deletado:"));
    let index = produtos.findIndex(p => p.id === id);

    if (index !== -1) {
        produtos.splice(index, 1);
        alert("Produto deletado com sucesso!");
    } else {
        alert("Produto não encontrado!");
    }
}

function visualizarProdutos() {
    let output = document.getElementById("output");
    output.innerHTML = "<h2>Lista de Produtos</h2>";

    if (produtos.length === 0) {
        output.innerHTML += "<p>Nenhum produto cadastrado.</p>";
    } else {
        let table = "<table><tr><th>ID</th><th>Nome</th><th>Quantidade</th><th>Valor</th><th>Data de Cadastro</th></tr>";
        produtos.forEach(produto => {
            table += `<tr>
                        <td>${produto.id}</td>
                        <td>${produto.nome}</td>
                        <td>${produto.quantidade}</td>
                        <td>${produto.valor}</td>
                        <td>${produto.dataCadastro}</td>
                      </tr>`;
        });
        table += "</table>";
        output.innerHTML += table;
    }
}
