# Objetos-Inteligentes-Conectados
Repositorio para o Projeto do sensor de temperatura da disciplina Objetos Inteligentes Conectados
Este projeto conta com uma placa ESP32 e um sensor DHT22 para monitorar as temperaturas e umidade do ambiente no qual ele se encontra, o projeto foi feito usando NODE-RED, InfluxDB e Grafana, para simular o sensor foi usado o ambiente do WOKWI.

###WOKWI: https://wokwi.com/projects/365260721147063297
Código:

//Incluir bibliotecas
#include <DHTesp.h>
#include <EspMQTTClient.h>

//Definicoes e constantes
char SSIDName[] = "Wokwi-GUEST"; 
char SSIDPass[] = ""; 

const int DHT_PIN = 15; 

char BrokerURL[] = "broker.hivemq.com";
char BrokerUserName[] = ""; 
char BrokerPassword[] = ""; 
char MQTTClientName[] = "HiveMQ"; 
int BrokerPort = 1883; 

String TopicoPrefixo = "TESTMACK32142293"; 
String Topico_01 = TopicoPrefixo+"/Temperatura"; 
String Topico_02 = TopicoPrefixo+"/Umidade"; 

//Variaveis globais e objetos
DHTesp dhtSensor;

EspMQTTClient clienteMQTT(SSIDName, SSIDPass, BrokerURL, BrokerUserName, BrokerPassword, MQTTClientName, BrokerPort); //inicializa o cliente MQTT

void onConnectionEstablished() {
}

void enviarDados() {
  TempAndHumidity temp_umid = dhtSensor.getTempAndHumidity();
    
  clienteMQTT.publish(Topico_01, String(temp_umid.temperature, 2) + "°C"); 
  clienteMQTT.publish(Topico_02, String(temp_umid.humidity, 1) + "%");
}

//Setup
void setup() {
  Serial.begin(9600);
  
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22); 

  clienteMQTT.enableDebuggingMessages();
}

//Loop
void loop() {
  clienteMQTT.loop();
  enviarDados(); 

  if (clienteMQTT.isWifiConnected() == 1) {
    Serial.println("Conectado ao WiFi!");
  } else {
    Serial.println("Nao conectado ao WiFi!");
  }

  if (clienteMQTT.isMqttConnected() == 1) {
    Serial.println("Conectado ao broker MQTT!");
  } else {
    Serial.println("Nao conectado ao broker MQTT!");
  }

  Serial.println("Nome do cliente: " + String(clienteMQTT.getMqttClientName())
    + " / Broker MQTT: " + String(clienteMQTT.getMqttServerIp())
    + " / Porta: " + String(clienteMQTT.getMqttServerPort())
  );

  delay(5000);
}
