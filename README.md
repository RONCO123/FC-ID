<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>App FC/ID Visual</title>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      padding: 20px;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #000428 0%, #004e92 100%);
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
    }

    h1 {
      color: #fff;
      margin-top: 20px;
      margin-bottom: 10px;
    }

    .section {
      background-color: rgba(255, 255, 255, 0.05);
      border-radius: 20px;
      padding: 20px;
      margin: 20px 0;
      width: 90%;
      max-width: 420px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }

    h2 {
      color: #fff;
      text-align: center;
    }

    input {
      padding: 12px;
      font-size: 18px;
      border: none;
      border-radius: 12px;
      width: 100%;
      margin-bottom: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }

    button {
      padding: 12px 24px;
      font-size: 18px;
      background-color: #00c6ff;
      color: white;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      width: 100%;
      margin-top: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.2);
    }

    button:hover {
      background-color: #007ea7;
    }

    .display {
      margin-top: 15px;
      font-family: 'Orbitron', monospace;
      font-size: 28px;
      background-color: #000;
      color: #00ffcc;
      padding: 15px 10px;
      border-radius: 12px;
      text-align: center;
      letter-spacing: 4px;
      box-shadow: 0 0 10px #00ffcc, 0 0 20px #00ffcc inset;
    }
  </style>
</head>
<body>

  <h1>App FC/ID</h1>

  <div class="section">
    <h2>Generar Código desde FC/ID</h2>
    <input type="number" id="fc" placeholder="Ingresa el FC (0-255)" />
    <input type="number" id="id" placeholder="Ingresa el ID (0-65535)" />
    <button onclick="generarCodigo()">Generar Código</button>
    <div id="resultadoGenerar" class="display">---</div>
  </div>

  <div class="section">
    <h2>Calcular FC/ID desde Código</h2>
    <input type="number" id="codigo" placeholder="Ingresa el código" />
    <button onclick="calcular()">Calcular</button>
    <div id="resultadoCalcular" class="display">---</div>
  </div>

  <script>
    function generarCodigo() {
      const fc = parseInt(document.getElementById("fc").value);
      const id = parseInt(document.getElementById("id").value);
      if (isNaN(fc) || isNaN(id) || fc < 0 || fc > 255 || id < 0 || id > 65535) {
        document.getElementById("resultadoGenerar").innerText = "ERROR";
        return;
      }
      const binFC = fc.toString(2).padStart(8, '0');
      const binID = id.toString(2).padStart(16, '0');
      const binTotal = binFC + binID;
      const codigo = parseInt(binTotal, 2);
      document.getElementById("resultadoGenerar").innerText = `CÓDIGO: ${codigo}`;
    }

    function calcular() {
      const codigo = parseInt(document.getElementById("codigo").value);
      if (isNaN(codigo)) {
        document.getElementById("resultadoCalcular").innerText = "ERROR";
        return;
      }
      const binario = codigo.toString(2).padStart(24, '0');
      const fc = parseInt(binario.slice(0, 8), 2);
      const id = parseInt(binario.slice(8), 2);
      document.getElementById("resultadoCalcular").innerText = `FC: ${fc} | ID: ${id}`;
    }
  </script>

</body>
</html>