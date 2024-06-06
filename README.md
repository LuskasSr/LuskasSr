
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CANDY BAY</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>CANDY BAY</h1>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#produtos">Produtos</a></li>
                <li><a href="#sobre">Sobre</a></li>
                <li><a href="#contato">Contato</a></li>
                <li><a href="#carrinho">Carrinho (<span id="carrinho-contagem">0</span>)</a></li>
            </ul>
        </nav>
    </header>
    <section id="home">
        <h2>Bem-vindo ao CANDY BAY</h2>
        <p>Os melhores doces online para você!</p>
    </section>
    <section id="produtos">
        <h2>Nossos Produtos</h2>
        <div class="produto">
            <img src="caminho/para/imagem-doce1.jpg" alt="Doce 1">
            <h3>Doce 1</h3>
            <p>Descrição do Doce 1</p>
            <button class="adicionar-carrinho" data-nome="Doce 1" data-preco="10.00">Adicionar ao Carrinho</button>
        </div>
        <div class="produto">
            <img src="caminho/para/imagem-doce2.jpg" alt="Doce 2">
            <h3>Doce 2</h3>
            <p>Descrição do Doce 2</p>
            <button class="adicionar-carrinho" data-nome="Doce 2" data-preco="12.00">Adicionar ao Carrinho</button>
        </div>
        <!-- Adicione mais produtos conforme necessário -->
    </section>
    <section id="sobre">
        <h2>Sobre Nós</h2>
        <p>Informações sobre a loja e a história.</p>
    </section>
    <section id="contato">
        <h2>Contato</h2>
        <form action="enviar_formulario.php" method="post">
            <label for="nome">Nome:</label>
            <input type="text" id="nome" name="nome" required>
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required>
            <label for="mensagem">Mensagem:</label>
            <textarea id="mensagem" name="mensagem" required></textarea>
            <button type="submit">Enviar</button>
        </form>
    </section>
    <section id="carrinho">
        <h2>Seu Carrinho</h2>
        <ul id="carrinho-lista"></ul>
        <p>Total: R$ <span id="carrinho-total">0.00</span></p>
    </section>
    <footer>
        <p>&copy; 2024 CANDY BAY. Todos os direitos reservados.</p>
    </footer>
    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f5f5f5;
    color: #333;
}

header {
    background-color: #ff69b4;
    padding: 20px;
    text-align: center;
    color: white;
    position: fixed;
    width: 100%;
    top: 0;
    z-index: 1000;
}

header h1 {
    margin: 0;
}

nav ul {
    list-style: none;
    padding: 0;
}

nav ul li {
    display: inline;
    margin: 0 15px;
}

nav ul li a {
    color: white;
    text-decoration: none;
}

section {
    padding: 80px 20px;
}

.produto {
    border: 1px solid #ddd;
    padding: 10px;
    margin: 10px 0;
    background-color: white;
    text-align: center;
}

.produto img {
    max-width: 100%;
    height: auto;
}

form {
    display: flex;
    flex-direction: column;
}

form label {
    margin-top: 10px;
}

form input, form textarea {
    padding: 10px;
    margin-top: 5px;
    border: 1px solid #ddd;
    border-radius: 5px;
}

form button {
    padding: 10px;
    margin-top: 10px;
    background-color: #ff69b4;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

form button:hover {
    background-color: #ff1493;
}

footer {
    background-color: #ff69b4;
    color: white;
    text-align: center;
    padding: 10px 0;
    position: fixed;
    bottom: 0;
    width: 100%;
}

// Smooth scroll para navegação
document.querySelectorAll('nav ul li a').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
        e.preventDefault();
        document.querySelector(this.getAttribute('href')).scrollIntoView({
            behavior: 'smooth'
        });
    });
});

// Carrinho de compras
let carrinho = [];
const carrinhoContagem = document.getElementById('carrinho-contagem');
const carrinhoLista = document.getElementById('carrinho-lista');
const carrinhoTotal = document.getElementById('carrinho-total');

document.querySelectorAll('.adicionar-carrinho').forEach(button => {
    button.addEventListener('click', function() {
        const nome = this.getAttribute('data-nome');
        const preco = parseFloat(this.getAttribute('data-preco'));
        const produto = { nome, preco };

        carrinho.push(produto);
        atualizarCarrinho();
    });
});

function atualizarCarrinho() {
    carrinhoContagem.textContent = carrinho.length;
    carrinhoLista.innerHTML = '';
    let total = 0;

    carrinho.forEach(produto => {
        const li = document.createElement('li');
        li.textContent = `${produto.nome} - R$ ${produto.preco.toFixed(2)}`;
        carrinhoLista.appendChild(li);
        total += produto.preco;
    });

    carrinhoTotal.textContent = total.toFixed(2);
}
