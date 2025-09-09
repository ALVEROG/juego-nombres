<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Juego de Nombres</title>
  <style>
    body { font-family: Arial, sans-serif; text-align: center; padding: 20px; }
    h1 { color: #333; }
    input, button { padding: 10px; font-size: 16px; margin: 10px; }
    #resultado { margin-top: 20px; font-size: 20px; font-weight: bold; color: darkblue; }
  </style>
</head>
<body>
  <h1>Juego de Nombres</h1>
  <p>Escribe tu nombre para participar:</p>
  <input type="text" id="miNombre" placeholder="Tu nombre aquí">
  <button onclick="sortear()">¡Dame mi nombre!</button>
  <div id="resultado"></div>

  <script>
    // 👉 Aquí defines los nombres participantes (máx 20)
    const nombres = [
      "Adrian", "Gianella", "Gisella", "Maricrys", "Alveiro", "Javier", "Mafe"
      "Carol", "Alejo", "Norys", "Ligia", "Merlyn", "Diana", "Camilo"
    ];

    function sortear() {
      const miNombre = document.getElementById("miNombre").value.trim();
      const resultadoDiv = document.getElementById("resultado");

      if (!miNombre) {
        resultadoDiv.innerText = "⚠️ Por favor escribe tu nombre primero.";
        return;
      }

      // Claves en localStorage
      const claveJugador = "resultado_" + miNombre.toLowerCase();
      const claveUsados = "usados_global";

      // Verificar si ya jugó antes
      const asignado = localStorage.getItem(claveJugador);
      if (asignado) {
        resultadoDiv.innerText = "✅ Ya tu nombre salió y te tocó: " + asignado;
        return;
      }

      // Recuperar lista de usados
      let usados = JSON.parse(localStorage.getItem(claveUsados) || "[]");

      // Filtrar nombres válidos (sin el propio y sin los ya usados)
      const posibles = nombres.filter(n =>
        n.toLowerCase() !== miNombre.toLowerCase() &&
        !usados.includes(n)
      );

      if (posibles.length === 0) {
        resultadoDiv.innerText = "⚠️ Ya no quedan nombres disponibles.";
        return;
      }

      // Escoger aleatorio
      const elegido = posibles[Math.floor(Math.random() * posibles.length)];

      // Guardar resultados
      localStorage.setItem(claveJugador, elegido);
      usados.push(elegido);
      localStorage.setItem(claveUsados, JSON.stringify(usados));

      // Mostrar resultado
      resultadoDiv.innerText = "🎉 Te tocó: " + elegido;
    }
  </script>
</body>
</html># juego-nombres
Juego de nombres para amigo secreto
