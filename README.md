# Validaci-n-de-C-dula
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Validación de Cédula - Algoritmo Módulo 10</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #333;
            text-align: center;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            box-sizing: border-box;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            font-size: 16px;
            margin-top: 10px;
        }
        button:hover {
            background-color: #45a049;
        }
        #result {
            margin-top: 20px;
            padding: 15px;
            text-align: center;
            display: none;
        }
        .correct {
            background-color: #dff0d8;
            color: #3c763d;
            border: 1px solid #d6e9c6;
            border-radius: 5px;
        }
        .incorrect {
            background-color: #f2dede;
            color: #a94442;
            border: 1px solid #ebccd1;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Validación de Cédula</h1>
        <p>Utilizando el algoritmo del módulo 10, validar si una cédula es correcta.</p>
        
        <div class="form-group">
            <label for="cedula">Ingrese la cédula (solo números):</label>
            <input type="text" id="cedula" placeholder="Ej: 1234567890" maxlength="11">
        </div>
        
        <button id="validateBtn">Validar Cédula</button>
        
        <div id="result"></div>
    </div>

    <script>
        // Evento para el botón de validar
        document.getElementById('validateBtn').addEventListener('click', validateCedula);
        
        function validateCedula() {
            // Obtener el valor de la cédula
            const cedula = document.getElementById('cedula').value.trim();
            
            // Validar que la cédula tenga 11 dígitos
            if (cedula.length !== 11) {
                showError('La cédula debe contener exactamente 11 dígitos.');
                return;
            }
            
            // Validar que la cédula contenga solo números
            if (!/^\d+$/.test(cedula)) {
                showError('La cédula debe contener solo números.');
                return;
            }
            
            // Extraer los dígitos de la cédula
            const digits = cedula.split('').map(Number);
            
            // Calcular el dígito verificador
            let sum = 0;
            for (let i = 0; i < 10; i++) {
                const digit = digits[i];
                let multiplied = digit * (i % 2 === 0 ? 1 : 2);
                
                if (multiplied > 9) {
                    multiplied = multiplied % 10 + 1;
                }
                
                sum += multiplied;
            }
            
            const remainder = sum % 10;
            const checkDigit = remainder === 0 ? 0 : 10 - remainder;
            
            // Validar el dígito verificador
            if (digits[10] === checkDigit) {
                showResult('CÉDULA ES CORRECTA', true);
            } else {
                showResult('CÉDULA ES INCORRECTA', false);
            }
        }
        
        function showResult(message, isValid) {
            const resultDiv = document.getElementById('result');
            resultDiv.style.display = 'block';
            resultDiv.textContent = message;
            
            if (isValid) {
                resultDiv.className = 'correct';
            } else {
                resultDiv.className = 'incorrect';
            }
        }
        
        function showError(message) {
            const resultDiv = document.getElementById('result');
            resultDiv.style.display = 'block';
            resultDiv.textContent = message;
            resultDiv.className = 'incorrect';
        }
    </script>
</body>
</html>
