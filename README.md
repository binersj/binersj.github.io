<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Água alunos Senac</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        .container {
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            width: 100%;
        }
        input, button {
            margin-bottom: 10px;
            padding: 10px;
            width: 100%;
            box-sizing: border-box;
        }
        button {
            background-color: #28a745;
            color: #fff;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        .illustration {
            text-align: center;
            margin-top: 20px;
        }
        .illustration img {
            max-width: 100%;
            height: auto;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Calculadora de Água Alunos Senac</h1>
        <form id="waterCalculator">
            <label for="weight">Peso (kg):</label>
            <input type="number" id="weight" min="1" required>
            <label for="age">Idade:</label>
            <input type="number" id="age" min="1" required>
            <label for="height">Altura (cm):</label>
            <input type="number" id="height" min="1" required>
            <label for="consumed">Água já bebida aprx (ml):</label>
            <input type="number" id="consumed" min="0" required>
            <button type="button" onclick="calculateWater()">Calcular</button>
        </form>
        <p id="result"></p>
        <div class="illustration">
            <img src="https://img.freepik.com/premium-vector/cute-calculator-with-glass-water-vector-cartoon-character-isolated-background_97231-2760.jpg" alt="Ilustração de Água">
        </div>
    </div>

    <script>
        function calculateWater() {
            const weight = parseFloat(document.getElementById('weight').value);
            const age = parseFloat(document.getElementById('age').value);
            const height = parseFloat(document.getElementById('height').value);
            const consumed = parseFloat(document.getElementById('consumed').value);
            
            if (isNaN(weight) || isNaN(age) || isNaN(height) || isNaN(consumed) || weight <= 0 || age <= 0 || height <= 0) {
                alert('Por favor, preencha todos os campos com valores válidos.');
                return;
            }
            
            // Fórmula simplificada para cálculo de água recomendada
            let recommendedWater = weight * 0.033; // Aproximadamente 33 ml por kg

            // Ajuste para idade
            if (age < 18) {
                recommendedWater *= 1.1; // Aumenta a recomendação para menores de 18 anos
            } else if (age > 60) {
                recommendedWater *= 0.9; // Diminui a recomendação para maiores de 60 anos
            }

            // Ajuste para altura (opcional, baseado em dados gerais)
            recommendedWater += (height - 160) * 0.01; // Aumenta ou diminui baseado na altura média de 160 cm

            // Calcula quanto falta
            const remainingWater = Math.max(0, recommendedWater - (consumed / 1000)); // converte ml para litros

            document.getElementById('result').innerText = 
                `Você deve beber aproximadamente ${recommendedWater.toFixed(2)} litros de água por dia. Já bebeu ${consumed / 1000} litros. Faltam ${remainingWater.toFixed(2)} litros para atingir sua meta diária.`;
        }
    </script>
</body>
</html>
