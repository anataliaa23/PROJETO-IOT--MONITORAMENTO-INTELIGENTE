# PROJETO-IOT--MONITORAMENTO-INTELIGENTE
DOCUMENTAÇÕES DO PROJETO DE IOT


### NOME DO PROJETO: 
**Monitoramento Inteligente do Ambiente: Medidas de Temperatura e Umidade com Arduino**

### DESCRIÇÃO & OBJETIVOS: 

O projeto tem como objetivo monitorar as condições de temperatura e umidade em um ambiente, utilizando uma placa Arduino em conjunto com sensores de temperatura/umidade e de movimento. 
O principal objetivo deste sistema é comparar os dados de temperatura e umidade do ambiente com os valores ideais para o bem-estar humano, fornecendo uma análise visual clara. 
A proposta envolve a utilização de LEDs coloridos e um display LCD, que oferecem em tempo real a visualização dos dados de temperatura e umidade. 
Além disso, é realizada a comunicação serial entre dispositivos e um módulo Bluetooth, garantindo que os dados também sejam exibidos no terminal do aplicativo SSP.
Esse sistema permitirá uma visualização clara das condições do ambiente e ajudará a manter um ambiente mais confortável e seguro.

### MATERIAIS UTILIZADOS

* Placa Arduino Uno
* Módulo de Sensor DHT11
* Módulo de Sensor PIR
* Display LCD I2C (16x2)
* LEDs (azul, vermelho e verde)
* Módulo Bluetooth HC-05
* Protoboard
* Fios de jumper (macho, macho x fêmea)
* Resistores

### ORGANIZAÇÃO ELETRÔNICA

* **Display LCD I2C**
  - SDA: PINO A4 
  - SCL: PINO A5 
  - VCC: 5V
  - GND: GND

* **Sensor DHT11**
  - Dados: PINO 7 (digital)
  - VCC: 5V
  - GND: GND

* **Sensor PIR**
  - Pino de sinal: PINO 13 (digital)
  - VCC: 5V
  - GND: GND

* **LEDs**
  - LED Vermelho (Temperatura Alta): PINO 6 (digital)
  - LED Verde (Temperatura Ideal): PINO 5 (digital)
  - LED Azul (Temperatura Baixa): PINO 4 (digital)
  - LED Vermelho (Umidade Alta): PINO 12 (digital)
  - LED Verde (Umidade Ideal): PINO 11 (digital)
  - LED Azul (Umidade Baixa): PINO 10 (digital)
  - **Todos conectados ao GND através de resistores.**

* **Módulo Bluetooth**
  - RX: PINO 8 (digital)
  - TX: PINO 9 (digital)
  - VCC: 5V
  - GND: GND
  - **Existem resistores para equilibrar a tensão.**

### DESCRIÇÃO DO ALGORITMO

O algoritmo segue a lógica de monitoramento de temperatura e umidade em um ambiente, ativando-se ao detectar movimento, conforme as instalações dos componentes listados acima. 
A estrutura do código é descrita da seguinte maneira:

1. **Inclusão e inicialização das bibliotecas necessárias**
   - `LiquidCrystal_I2C.h` (comunicação I2C para o display LCD)
   - `DHT.h` (leitura de temperatura e umidade)
   - `SoftwareSerial.h` (comunicação Bluetooth)
   - Além de outras funções incluídas na biblioteca padrão.

2. **Definição dos pinos dos sensores, LEDs e constantes de temperatura e umidade.**

3. **Inicialização no setup()**
   - O display LCD e os sensores são inicializados, assim como a configuração dos pinos de entrada e saída. A comunicação serial e a comunicação via Bluetooth também são iniciadas.

4. **Loop principal**
   - O programa entra em um loop contínuo onde:
     - Lê o estado do sensor PIR (detector de movimento).
   - Se movimento for detectado:
       - Limpa o display LCD e exibe "Movimento Detectado".
       - Lê a temperatura e umidade do sensor DHT, armazenando em variáveis.
       - Verifica se a leitura é válida (NaN). Se for, continua; se não, exibe uma mensagem de "erro de leitura".
       - Se a leitura for válida, mostra a temperatura e umidade no display LCD.
       - Envia os dados via Bluetooth e pela porta serial em formato de string.
       - Controla os LEDs de acordo com a temperatura e umidade, acendendo ou apagando conforme os limites definidos.
     - Avalia os valores de temperatura e umidade para controlar os LEDs:
       - Se a temperatura for igual ou maior que o limite alto, um LED vermelho é aceso, e os outros são apagados.
       - Se a temperatura for maior que o limite baixo e menor que limite alto, um LED verde é aceso, e os outros são apagados.
       - Se a temperatura for igual ou menor que o limite baixo, um LED azul é aceso, e os outros são apagados.
     - O mesmo se aplica à umidade, com LEDs correspondentes para altas, ideais e baixas leituras.
 - Se não houver movimento, o display exibe "Sem Movimento".
     

5. **Utilização de temporizadores**
   - O algoritmo usa temporizadores para controlar a exibição de mensagens e a frequência de leitura dos sensores.
