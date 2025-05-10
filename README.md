<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Encuesta de Estrés</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body { font-family: Arial; margin: 20px; }
    .question { margin-bottom: 15px; }
    button { margin-top: 20px; padding: 10px 20px; }
    canvas { max-width: 600px; }
  </style>
</head>
<body>
  <h2>Encuesta de Nivel de Estrés</h2>
  
  <form id="stressForm">
    <div class="question">
      <label>1. ¿Con qué frecuencia sientes que estás bajo presión?</label><br>
      <select name="q1">
        <option value="0">Nunca</option>
        <option value="1">Rara vez</option>
        <option value="2">A veces</option>
        <option value="3">Frecuentemente</option>
        <option value="4">Siempre</option>
      </select>
    </div>

    <div class="question">
      <label>2. ¿Te sientes con la capacidad para relajarte después de un día agitado?</label><br>
      <select name="q2">
        <option value="4">Nunca</option>
        <option value="3">Rara vez</option>
        <option value="2">A veces</option>
        <option value="1">Frecuentemente</option>
        <option value="0">Siempre</option>
      </select>
    </div>

    <div class="question">
      <label>3. ¿Con qué frecuencia sientes que no puedes desconectarte mentalmente del trabajo?</label><br>
      <select name="q3">
        <option value="0">Nunca</option>
        <option value="1">Rara vez</option>
        <option value="2">A veces</option>
        <option value="3">Frecuentemente</option>
        <option value="4">Siempre</option>
      </select>
    </div>

    <div class="question">
      <label>4. ¿Qué tan seguido sientes que no tienes el control sobre tu vida?</label><br>
      <select name="q4">
        <option value="0">Nunca</option>
        <option value="1">Rara vez</option>
        <option value="2">A veces</option>
        <option value="3">Frecuentemente</option>
        <option value="4">Siempre</option>
      </select>
    </div>

    <div class="question">
      <label>5. ¿Con qué frecuencia pierdes la paciencia?</label><br>
      <select name="q5">
        <option value="0">Nunca</option>
        <option value="1">Rara vez</option>
        <option value="2">A veces</option>
        <option value="3">Frecuentemente</option>
        <option value="4">Siempre</option>
      </select>
    </div>

    <button type="button" onclick="calcularEstres()">Ver Resultado</button>
  </form>

  <div style="margin-top: 40px;">
    <canvas id="graficaEstres"></canvas>
  </div>

  <script>
    function calcularEstres() {
      const form = document.forms['stressForm'];
      let puntaje = 0;
      for (let i = 1; i <= 5; i++) {
        puntaje += parseInt(form[`q${i}`].value);
      }

      const nivel = puntaje <= 6 ? "Bajo" :
                    puntaje <= 12 ? "Moderado" : "Alto";

      const ctx = document.getElementById('graficaEstres').getContext('2d');

      if (window.grafico) {
        window.grafico.destroy();
      }

      window.grafico = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: ['Puntaje de Estrés'],
          datasets: [{
            label: `Nivel: ${nivel}`,
            data: [puntaje],
            backgroundColor: nivel === "Bajo" ? 'green' : nivel === "Moderado" ? 'orange' : 'red'
          }]
        },
        options: {
          scales: {
            y: { beginAtZero: true, max: 20 }
          }
        }
      });
    }
  </script>
</body>
</html>
