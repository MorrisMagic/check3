<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="weather-app">
        <h1>Weather App</h1>
        <input type="text" id="city" placeholder="Enter city">
        <button id="getWeather">Get Weather</button>
        <div id="weatherDisplay">
            <h2 id="location"></h2>
            <p id="temperature"></p>
            <p id="description"></p>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>


body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background: #f0f0f0;
}

.weather-app {
    background: #fff;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

input {
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
    margin-right: 10px;
}

button {
    padding: 10px 15px;
    background-color: #3498db;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #2980b9;
}

#weatherDisplay {
    margin-top: 20px;
}

#location {
    font-size: 24px;
    font-weight: bold;
}

#temperature, #description {
    font-size: 18px;
}

@media (max-width: 600px) {
    .weather-app {
        width: 100%;
        padding: 15px;
    }
}
document.getElementById('getWeather').addEventListener('click', getWeather);

async function getWeather() {
    const city = document.getElementById('city').value;
    const apiKey = 'your_openweathermap_api_key'; // Replace with your OpenWeatherMap API key
    const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

    try {
        const response = await fetch(url);
        if (!response.ok) {
            throw new Error('City not found');
        }

        const data = await response.json();
        displayWeather(data);
    } catch (error) {
        alert(error.message);
    }
}

function displayWeather(data) {
    document.getElementById('location').textContent = `${data.name}, ${data.sys.country}`;
    document.getElementById('temperature').textContent = `Temperature: ${data.main.temp}°C`;
    document.getElementById('description').textContent = `Description: ${data.weather[0].description}`;
}
