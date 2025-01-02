# Coroinhas-
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Site de Votação</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 500px;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        p.descricao {
            font-size: 14px;
            color: #555;
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin: 10px 0 5px;
        }
        select {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        .results {
            margin-top: 20px;
        }
        .results div {
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Vote no Coroinha Estrela</h1>
        <p class="descricao">E para iniciar, vamos premiar o coroinha que tem um calendário tão exclusivo quanto o de uma estrela de cinema! O 'Coroinha Estrela' é aquele que só aparece em solenidades especiais, como se fosse um VIP das missas. Quando ele entra, a igreja até ilumina, e todos ficam se perguntando: 'Será que é ele mesmo?'. Esse coroinha só surge para as grandes ocasiões, e quando chega, é como um show à parte. Se ele aparecer, pode esperar: é uma solenidade de verdade! E o prêmio vai para...</p>

        <label for="coroinha1">Escolha o Coroinha 1</label>
        <select id="coroinha1" onchange="registrarVoto('opcao1', this.value, 3)">
            <option value="">Selecione um coroinha</option>
        </select>

        <label for="coroinha2">Escolha o Coroinha 2</label>
        <select id="coroinha2" onchange="registrarVoto('opcao2', this.value, 2)">
            <option value="">Selecione um coroinha</option>
        </select>

        <label for="coroinha3">Escolha o Coroinha 3</label>
        <select id="coroinha3" onchange="registrarVoto('opcao3', this.value, 1)">
            <option value="">Selecione um coroinha</option>
        </select>

        <div class="results" id="resultados"></div>
    </div>

    <script>
        // Base de dados dos coroinhas
        const coroinhas = ["João", "Maria", "Pedro", "Ana", "Carlos", "Lucas", "Paula", "Tiago", "Mariana"];

        // Armazenar os pontos de cada coroinha
        const pontos = {};

        // Preenche os dropdowns com os nomes dos coroinhas
        function preencherDropdowns() {
            const dropdowns = ["coroinha1", "coroinha2", "coroinha3"];
            dropdowns.forEach(id => {
                const select = document.getElementById(id);
                coroinhas.forEach(coroinha => {
                    const option = document.createElement('option');
                    option.value = coroinha;
                    option.textContent = coroinha;
                    select.appendChild(option);
                });
            });
        }

        // Registra o voto ao selecionar
        function registrarVoto(opcao, nome, pontosPorPosicao) {
            if (!nome) return;

            // Adiciona os pontos ao coroinha
            if (!pontos[nome]) {
                pontos[nome] = 0;
            }
            pontos[nome] += pontosPorPosicao;

            // Atualiza os resultados para o administrador
            exibirResultados();
        }

        // Exibe os resultados para o administrador
        function exibirResultados() {
            const resultadosDiv = document.getElementById('resultados');
            const coroinhasOrdenados = Object.entries(pontos)
                .sort((a, b) => b[1] - a[1]) // Ordena por pontos, do maior para o menor
                .map(entry => `${entry[0]}: ${entry[1]} pontos`)
                .join('<br>');

            // Exibe os resultados
            resultadosDiv.innerHTML = `
                <h2>Resultado Final (apenas para administrador):</h2>
                <div>${coroinhasOrdenados}</div>
            `;
        }

        // Preenche os dropdowns ao carregar a página
        window.onload = preencherDropdowns;
    </script>
</body>
</html>
