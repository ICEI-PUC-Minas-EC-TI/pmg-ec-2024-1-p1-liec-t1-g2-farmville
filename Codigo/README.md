// Definindo os pinos
const int sensorPin = A0; // Pino analógico para o sensor de umidade
const int relayPin = 8;   // Pino digital para o relé
const int threshold = 500; // Limite de umidade do solo

void setup() {
  // Inicializa o pino do relé como saída
  pinMode(relayPin, OUTPUT);
  // Inicializa a comunicação serial para monitoramento
  Serial.begin(9600);
}

void loop() {
  // Leitura do valor do sensor de umidade
  int sensorValue = analogRead(sensorPin);
  // Imprime o valor do sensor no monitor serial
  Serial.print("Umidade do Solo: ");
  Serial.println(sensorValue);

  // Verifica se o valor está abaixo do limite
  if (sensorValue < threshold) {
    // Aciona a bomba de água
    digitalWrite(relayPin, LOW); // Ativa o relé (assumindo que LOW liga o relé)
    Serial.println("Bomba Ligada");
  } else {
    // Desliga a bomba de água
    digitalWrite(relayPin, HIGH); // Desativa o relé (assumindo que HIGH desliga o relé)
    Serial.println("Bomba Desligada");
  }

  // Aguarda por um segundo antes de repetir a leitura
  delay(1000);
}
