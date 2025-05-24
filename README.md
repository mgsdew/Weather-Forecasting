Weather forecasting is vital for environmental monitoring, agricultural planning, and early warning systems, aiding in environmental assessment, cultivation planning, and hazard mitigation. Where, the Raspberry Pi offers a cost-effective solution for weather forecasting, but its standard setups often lack autonomous forecasting features, limiting its potential. 
Also, Machine learning applications offer a promising alternative to traditional physics-based weather prediction frameworks, efficiently analyzing complex temporal trends using environmental datasets. 

In this project I use below tools for a weather predictions: -

1.  Raspberry Pi 4B, Node-RED, and CatBoost ML.
2.  Secure MQTT (TLS) messaging via EMQX broker.
3.  48-hour forecast with real-time visualization and alarms.

Weather data taken from public API OpenWeatherMap (https://openweathermap.org/), and stored collected data using JSON-based format in InfluxDB database with JSON structure.

System Architecture: 
-------------------

   Flow the system likes below: -

1. Node-RED flows orchestrate Python ML functions.
2. Data pipeline: API → Node-RED → InfluxDB → ML model → MQTT.
3. TLS-secured MQTT publishes forecast, live data, alarms.

![image](https://github.com/user-attachments/assets/7b24f772-304a-49cb-a47d-51836ef64335)


Forecast Model
--------------

1. CatBoost regression predicts 48-hour temperature.

2. Trained on 7-day window using time series data.

3. Optuna used for model tuning.

![image](https://github.com/user-attachments/assets/5676fbf5-1afa-48f9-83ce-c3360bd16376)


Prediction Accuracy
-------------------
Got an RMSE: 0.278 °C, R² Score: 0.9959 on model validated against actual API values.

Real-Time Visualization
-----------------------
Triggered if pressure drops ≥ 2 hPa within 6 hours.
![image](https://github.com/user-attachments/assets/04f0b3e1-7812-4fba-9cf1-5341da4823c6)


Security Features
------------------

1. Used MQTT secured with TLS over port 8883.
2. QoS level 1, for retaining messages.
3. Node-RED UI secured with HTTPS and login.













