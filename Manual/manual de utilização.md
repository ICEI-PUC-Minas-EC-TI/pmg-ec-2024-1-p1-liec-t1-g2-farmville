
## Instruções de utilização

Para complementar o projeto de irrigação automática de água com as instruções de utilização, aqui está um guia detalhado sobre como configurar o hardware e software, além de informações importantes para executar o projeto.

## Configuração do Hardware

### Componentes Necessários
1. *Microcontrolador* (Arduino)
2. *Sensor de Umidade do Solo*
3. *Relé*
4. *Bomba de Água*
5. *Reservatório de Água*
6. *Tubulação*
7. *Fonte de Alimentação* (compatível com o microcontrolador e a bomba de água)
8. *Conectores e Fios*
9. *Placa de Protoboard* (para prototipagem, se necessário)
10. *Valvulas solenoides* (opcional, dependendo do projeto)

### Montagem
1. *Sensor de Umidade do Solo*:
   - Conecte o sensor ao microcontrolador. Normalmente, ele tem três pinos: VCC (alimentação), GND (terra) e SIG (sinal). Conecte VCC ao 3.3V ou 5V do microcontrolador, GND ao GND e SIG a um pino analógico (ex.: A0 no Arduino).

2. *Relé*:
   - Conecte a bobina do relé ao microcontrolador. O relé tem pinos VCC, GND e IN. Conecte VCC ao 5V, GND ao GND, e IN a um pino digital (ex.: D7 no Arduino).

3. *Bomba de Água*:
   - Conecte a bomba de água ao relé. A bomba de água terá dois fios de alimentação que deverão ser conectados aos terminais COM e NO (normalmente aberto) do relé.

4. *Fonte de Alimentação*:
   - Conecte a fonte de alimentação ao microcontrolador e à bomba de água, conforme necessário.

5. *Tubulação e Reservatório*:
   - Conecte a tubulação à saída da bomba de água e ao sistema de irrigação. Assegure-se de que o reservatório de água esteja posicionado de modo que a bomba possa puxar a água adequadamente.

## Configuração do Software

### Instalação do Ambiente de Desenvolvimento
1. *Arduino IDE* (ou outra IDE compatível com o microcontrolador):
   - Faça o download e instale o Arduino IDE a partir do site oficial: [Arduino IDE](https://www.arduino.cc/en/software).

2. *Bibliotecas Necessárias*:
   - Se estiver utilizando um microcontrolador específico, instale a biblioteca correspondente (ex.: ESP8266 ou ESP32):
     - No Arduino IDE, vá para Sketch > Include Library > Manage Libraries.
     - Procure pela biblioteca necessária e clique em Install.

### Código de Controle
cpp
// Definições de pinos
const int soilMoisturePin = A0; // Pino analógico para o sensor de umidade do solo
const int relayPin = 7; // Pino digital para o relé

// Nível de umidade mínima antes de acionar a irrigação
const int moistureThreshold = 300;

void setup() {
  Serial.begin(9600); // Inicializa a comunicação serial
  pinMode(soilMoisturePin, INPUT);
  pinMode(relayPin, OUTPUT);
  digitalWrite(relayPin, LOW); // Inicializa o relé como desligado
}

void loop() {
  int soilMoistureValue = analogRead(soilMoisturePin); // Leitura do sensor de umidade
  Serial.print("Umidade do Solo: ");
  Serial.println(soilMoistureValue);

  if (soilMoistureValue < moistureThreshold) {
    digitalWrite(relayPin, HIGH); // Liga a bomba de água
    Serial.println("Bomba ligada");
  } else {
    digitalWrite(relayPin, LOW); // Desliga a bomba de água
    Serial.println("Bomba desligada");
  }

  delay(1000); // Espera 1 segundo antes da próxima leitura
}


### Upload do Código
1. Conecte o microcontrolador ao computador via USB.
2. No Arduino IDE, selecione a placa correta e a porta COM correspondente.
3. Faça o upload do código clicando no botão Upload.

## Informações Importantes
- *Calibração do Sensor*: Antes de usar o sistema, calibre o sensor de umidade do solo. Coloque o sensor em solo seco e anote o valor lido, depois coloque em solo úmido e anote novamente. Ajuste o moistureThreshold conforme necessário.
- *Manutenção*: Verifique regularmente o sensor de umidade e a bomba de água para garantir que estejam funcionando corretamente.
- *Segurança*: Certifique-se de que todas as conexões elétricas estejam bem isoladas e que a fonte de alimentação seja adequada para evitar sobrecargas.

Com essas instruções, você deverá ser capaz de montar e configurar o seu sistema de irrigação automática de água com sucesso.
