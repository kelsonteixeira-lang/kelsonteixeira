<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StreamFilmes</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #000000;
            color: #ffffff;
        }
        header {
            background: #c8102e;
            color: #ffffff;
            padding: 10px 0;
            text-align: center;
        }
        nav {
            background: #d92027;
            margin: 20px;
            padding: 10px;
        }
        nav a {
            color: #ffffff;
            margin: 0 15px;
            text-decoration: none;
        }
        main {
            padding: 20px;
        }
        .planos, .filmes, .payment-container, .login-container, .signup-container {
            background: #1c1c1c;
            border-radius: 5px;
            padding: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        footer {
            text-align: center;
            padding: 20px;
            background: #c8102e;
            color: #ffffff;
            position: relative;
            bottom: 0;
            width: 100%;
        }
        h2 {
            text-align: center;
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 3px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #c8102e;
            color: #ffffff;
            border: none;
            border-radius: 3px;
            cursor: pointer;
        }
        button:hover {
            background-color: #a40e1d;
        }
    </style>
</head>
<body>
    <header>
        <h1>StreamFilmes</h1>
        <p>Assista a todos os seus filmes favoritos!</p>
    </header>
    <nav>
        <a href="#filmes" id="filmesLink">Filmes</a>
        <a href="#planos" id="planosLink">Planos</a>
        <a href="#login" id="loginLink">Login</a>
        <a href="#signup" id="signupLink">Criar Conta</a>
    </nav>
    <main>
        <div class="login-container" id="loginContainer">
            <h2>Login</h2>
            <form action="/login" method="POST">
                <label for="username">Nome de Usuário:</label>
                <input type="text" id="username" name="username" required>
                <label for="password">Senha:</label>
                <input type="password" id="password" name="password" required>
                <button type="submit">Entrar</button>
            </form>
        </div>

        <div class="signup-container" id="signupContainer">
            <h2>Criar Conta</h2>
            <form action="/signup" method="POST">
                <label for="newUsername">Nome de Usuário:</label>
                <input type="text" id="newUsername" name="newUsername" required>
                <label for="newPassword">Senha:</label>
                <input type="password" id="newPassword" name="newPassword" required>
                <button type="submit">Cadastrar</button>
            </form>
        </div>

        <section id="planos" class="planos">
            <h2>Nossos Planos</h2>
            <ul>
                <li>
                    <strong>Plano Mensal:</strong> € 1,99/mês
                    <button onclick="showPayment('month')">Assinar</button>
                </li>
                <li>
                    <strong>Plano Trimestral:</strong> € 2,50/3 meses
                    <button onclick="showPayment('quarter')">Assinar</button>
                </li>
                <li>
                    <strong>Plano Anual:</strong> € 23,00/anual
                    <button onclick="showPayment('year')">Assinar</button>
                </li>
            </ul>
            <p>Para assinar um plano, você deve fornecer os detalhes do cartão de crédito.</p>
        </section>

        <section id="filmes" class="filmes" style="display:none;">
            <h2>Filmes Disponíveis</h2>
            <p>Todos os filmes do mundo disponíveis! (Ainda em desenvolvimento...)</p>
            <p>Clique em um filme para ver detalhes, <strong>mas se você não tiver um plano, será redirecionado para a área de planos.</strong></p>
        </section>

        <div class="payment-container" id="paymentContainer" style="display:none;">
            <h2>Detalhes do Cartão de Crédito</h2>
            <form action="/payment" method="POST">
                <label for="cardName">Nome no Cartão:</label>
                <input type="text" id="cardName" name="cardName" required>
                <label for="cardNumber">Número do Cartão:</label>
                <input type="text" id="cardNumber" name="cardNumber" required>
                <label for="expiryDate">Data de Validade (MM/AA):</label>
                <input type="text" id="expiryDate" name="expiryDate" required>
                <label for="cvv">CVV:</label>
                <input type="text" id="cvv" name="cvv" required>
                <button type="submit">Confirmar Pagamento</button>
            </form>
        </div>
    </main>
    <footer>
        <p>&copy; 2023 StreamFilmes. Todos os direitos reservados.</p>
    </footer>

    <script>
        document.getElementById('loginLink').onclick = function() {
            document.getElementById('loginContainer').style.display = 'block';
            document.getElementById('signupContainer').style.display = 'none';
            document.getElementById('filmes').style.display = 'none';
            document.getElementById('planos').style.display = 'none';
            document.getElementById('paymentContainer').style.display = 'none';
        };

        document.getElementById('signupLink').onclick = function() {
            document.getElementById('signupContainer').style.display = 'block';
            document.getElementById('loginContainer').style.display = 'none';
            document.getElementById('filmes').style.display = 'none';
            document.getElementById('planos').style.display = 'none';
            document.getElementById('paymentContainer').style.display = 'none';
        };

        document.getElementById('filmesLink').onclick = function() {
            document.getElementById('filmes').style.display = 'block';
            document.getElementById('signupContainer').style.display = 'none';
            document.getElementById('loginContainer').style.display = 'none';
            document.getElementById('planos').style.display = 'none';
            document.getElementById('paymentContainer').style.display = 'none';
        };

        document.getElementById('planosLink').onclick = function() {
            document.getElementById('planos').style.display = 'block';
            document.getElementById('signupContainer').style.display = 'none';
            document.getElementById('loginContainer').style.display = 'none';
            document.getElementById('filmes').style.display = 'none';
            document.getElementById('paymentContainer').style.display = 'none';
        };

        function showPayment(plan) {
            document.getElementById('paymentContainer').style.display = 'block';
            document.getElementById('planos').style.display = 'none';
        }
    </script>
</body>
</html>
