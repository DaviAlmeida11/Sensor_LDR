🌟 Projeto: Sistema de Monitoramento de Luz com LDR e ESP32

Este repositório apresenta um sistema de detecção de luminosidade utilizando a plataforma ESP32 em conjunto com um sensor LDR (Light Dependent Resistor). O objetivo é automatizar o acionamento de um LED com base na intensidade de luz do ambiente.

📹 Vídeo demonstrativo: Sensor LDR em funcionamento

🧾 Descrição do Projeto

Este projeto explora o uso do conversor ADC (Analógico-Digital) do ESP32 para interpretar variações de luminosidade captadas pelo sensor LDR.

O LDR varia sua resistência de acordo com a luz ambiente.
O ESP32 realiza leitura analógica variando entre 0 e 4095.
Quando o valor lido fica abaixo de 400, o sistema entende que o ambiente está escuro.
Nesse caso, um LED é acionado automaticamente como luz de apoio/emergência.
As leituras são exibidas em tempo real pelo Monitor Serial.
🧰 Materiais Utilizados
Componente	Quantidade
ESP32 DevKit V1	1
Sensor LDR (módulo ou componente)	1
LED vermelho	1
Resistor 220Ω	1
Protoboard	1
Jumpers diversos	~7
🔌 Conexões do Circuito
📡 Sensor LDR
VCC → 3.3V ou VIN do ESP32
GND → GND
AO (Analógico) → GPIO 34
DO (Digital) → não utilizado
💡 LED
Ânodo (perna longa) → GPIO 32
Cátodo (perna curta) → Resistor 220Ω → GND
🔧 Observações

Alguns jumpers adicionais foram utilizados apenas para organização e distribuição de energia na protoboard.

⚙️ Configuração do Ambiente
Instale a Arduino IDE
Adicione a seguinte URL em Preferências > URLs adicionais de placas:
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
Instale o suporte ao ESP32 pelo Gerenciador de Placas
💻 Código do Projeto
/*
 * Projeto: Monitoramento de Luminosidade com LDR e ESP32
 * Desenvolvido por: Vitor Miguel, Kauan, Davi
 */

// Pinos utilizados
const int PINO_LDR = 34;
const int PINO_LED = 32;

// Limite para considerar ambiente escuro
const int LIMIAR_ESCURIDAO = 400;

void setup() {
  Serial.begin(115200);
  pinMode(PINO_LED, OUTPUT);
}

void loop() {
  int leituraLDR = analogRead(PINO_LDR);

  Serial.print("Luminosidade atual: ");
  Serial.println(leituraLDR);

  if (leituraLDR < LIMIAR_ESCURIDAO) {
    Serial.println("Ambiente escuro detectado. LED ligado.");
    digitalWrite(PINO_LED, HIGH);
  } else {
    Serial.println("Ambiente iluminado. LED desligado.");
    digitalWrite(PINO_LED, LOW);
  }

  delay(1000);
}