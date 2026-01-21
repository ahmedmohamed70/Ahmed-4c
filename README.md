<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <title>Meteo – Verifica</title>

    <!-- Stile semplice -->
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 30px;
        }
        input, button {
            padding: 5px;
            margin-top: 5px;
        }
        #output {
            margin-top: 15px;
        }
    </style>
</head>

<body>

<h2>Meteo attuale</h2>

<!-- Inserimento dati -->
<label>Latitudine:</label><br>
<input type="number" id="lat" step="0.0001"><br>

<label>Longitudine:</label><br>
<input type="number" id="lon" step="0.0001"><br><br>

<button onclick="mostraMeteo()">Mostra meteo</button>

<!-- Risultato -->
<div id="output"></div>

<script>
    // Funzione che prende i dati meteo
    function mostraMeteo() {

        // Legge i valori inseriti
        let lat = document.getElementById("lat").value;
        let lon = document.getElementById("lon").value;

        // Controllo se i campi sono vuoti
        if (lat == "" || lon == "") {
            alert("Inserisci latitudine e longitudine");
            return;
        }

        // URL dell'API Open-Meteo
        let url = "https://api.open-meteo.com/v1/forecast?latitude="
                  + lat + "&longitude=" + lon +
                  "&current_weather=true";

        // Richiesta dei dati
        fetch(url)
            .then(response => response.json())
            .then(data => {
                let meteo = data.current_weather;

                // Visualizzazione dei dati
                document.getElementById("output").innerHTML =
                    "Temperatura: " + meteo.temperature + " °C<br>" +
                    "Vento: " + meteo.windspeed + " km/h<br>" +
                    "Ora: " + meteo.time;
            });
    }
</script>

</body>
</html># Ahmed-4c