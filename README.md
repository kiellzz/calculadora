# terceiro-per-odo

<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>Calculadora Simples</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="calculadora">
        <h2>Calculadora</h2>
        <!-- Campo onde a expressão e o resultado vão ser exibidos -->
        <input type="text" id="display" placeholder="0" readonly>

        <div class="botoes">
            <!-- Botões -->
            <button onclick="inserirNoDisplay('7')">7</button>
            <button onclick="inserirNoDisplay('8')">8</button>
            <button onclick="inserirNoDisplay('9')">9</button>
            <button onclick="inserirNoDisplay('/')">/</button>

            <button onclick="inserirNoDisplay('4')">4</button>
            <button onclick="inserirNoDisplay('5')">5</button>
            <button onclick="inserirNoDisplay('6')">6</button>
            <button onclick="inserirNoDisplay('*')">*</button>

            <button onclick="inserirNoDisplay('1')">1</button>
            <button onclick="inserirNoDisplay('2')">2</button>
            <button onclick="inserirNoDisplay('3')">3</button>
            <button onclick="inserirNoDisplay('-')">-</button>

            <button onclick="inserirNoDisplay('0')">0</button>
            <button onclick="apagarUltimo()">Del</button>
            <button onclick="calcularExpressao()">=</button>
            <button onclick="inserirNoDisplay('+')">+</button>
        </div>
    </div>
     <p class="api-nome">API utilizada:
        <a href="https://mathjs.org/" target="_blank">math.js</a>
     </p>

    <script>
        // insere valor no display
        function inserirNoDisplay(valor) {
            const display = document.getElementById('display');
            display.value += valor;
        }

 // apaga o último caractere
        function apagarUltimo() {
            const display = document.getElementById('display');
            display.value = display.value.slice(0, -1);
        }

        // resultado da expressão
        async function calcularExpressao() {
            const display = document.getElementById('display');
            const expressao = display.value.trim();

            // display vazio = nada
            if (expressao === '') {
                return;
            }

            try {
                // API math.js
                const resposta = await fetch(`https://api.mathjs.org/v4/?expr=${encodeURIComponent(expressao)}`);
                
                if (!resposta.ok) {
                    throw new Error('Erro na resposta da API');
                }

                const resultado = await resposta.text();
                display.value = resultado;
            } catch (erro) {
                // em caso de erro, exibe a mensagem
                display.value = 'Erro';
                console.error('Erro ao calcular a expressão:', erro);
            }
        }
    </script>
    <div class="desenvolvido">
        <p>Desenvolvido por:Ezequiel Borges</p>
</body>
</html>

body {
    font-family: Arial, sans-serif;
    background: url('imgs/fundo');
    background-size: cover;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.calculadora {
    background: rgb(0, 0, 0);
    padding: 27px;
    border-radius: 10px;
    box-shadow: 0 0 10px #ccc;
    width: 240px;
    text-align: center;
}

#display {
    width: 100%;
    padding: 13px;
    font-size: 19px;
    margin-bottom: 12px;
    text-align: center;
     box-sizing: border-box
}

.botoes {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}

button {
    padding: 20px;
    font-size: 18px;
    cursor: pointer;
    border: none;
    border-radius: 5px;
    background-color: #e0e0e0;
    transition: background 0.2s;
    text-align: center;
}

button:hover {
    background-color: #d5d5d5;
}

.calculadora h2 {
    color: white;
}

.api-nome {
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    text-align: center;
    margin-top: 40px;
    color: #000000;
    font-size:14px;
    padding: 15px;
}

.desenvolvido {
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    text-align: center;
    margin-top: 0px;
    color: #000000;
    font-size: 16px;
}
