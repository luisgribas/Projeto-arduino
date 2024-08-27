
### Componentes Necessários

- **Arduino Uno**
- **LED Infravermelho (IR)**
- **Resistor de 220 ohms**
- **Botões**
- **Protoboard e fios de conexão**
- **Biblioteca `IRremote`**

### Esquema de Montagem

1. **Conecte o LED IR ao Arduino**:
   - **Anodo (perna longa) do LED IR** -> Pino Digital 3 do Arduino
   - **Catodo (perna curta) do LED IR** -> Resistor de 220 ohms -> GND do Arduino

2. **Conecte os Botões ao Arduino**:
   - **Botão 1** -> Pino Digital 2 do Arduino
   - **Botão 2** -> Pino Digital 4 do Arduino
   - Cada botão deve ser conectado a um pino digital com um resistor pull-down para garantir leitura correta.

### Código Arduino

```cpp
#include <IRremote.h>

const int irLedPin = 3;  // Pino do LED IR
const int buttonPin1 = 2; // Botão 1
const int buttonPin2 = 4; // Botão 2

IRsend irsend; // Cria uma instância da classe IRsend

void setup() {
  pinMode(buttonPin1, INPUT_PULLUP);  // Configura o pino do botão como entrada com pull-up interno
  pinMode(buttonPin2, INPUT_PULLUP);
  irsend.begin(); // Inicializa o emissor IR
}

void loop() {
  if (digitalRead(buttonPin1) == LOW) {
    // Envia um código IR quando o botão 1 é pressionado
    irsend.sendNEC(0x20DF10EF, 32);  // Código IR para o botão 1 (ajuste conforme necessário)
    delay(1000); // Aguarda 1 segundo para evitar múltiplos comandos
  }
  if (digitalRead(buttonPin2) == LOW) {
    // Envia um código IR quando o botão 2 é pressionado
    irsend.sendNEC(0x20DF40BF, 32);  // Código IR para o botão 2 (ajuste conforme necessário)
    delay(1000); // Aguarda 1 segundo para evitar múltiplos comandos
  }
}
```

### Como Testar o Código

1. **Instale a Biblioteca `IRremote`**:
   - Abra o Arduino IDE.
   - Vá em **Sketch > Incluir Biblioteca > Gerenciar Bibliotecas**.
   - Pesquise por "IRremote" e instale a biblioteca desenvolvida por `shirriff`.

2. **Carregue o Código no Arduino**:
   - Conecte o Arduino ao computador.
   - Selecione a placa e a porta no Arduino IDE.
   - Clique em "Upload" para carregar o código.

3. **Conecte o LED IR ao Arduino**:
   - Certifique-se de que o LED IR está posicionado em direção ao receptor IR da TV.

4. **Pressione os Botões**:
   - Pressione os botões conectados aos pinos digitais do Arduino para enviar comandos à TV.

### Notas Adicionais

- **Códigos IR**: O código fornecido usa códigos IR genéricos (0x20DF10EF e 0x20DF40BF) que são exemplos. Para obter os códigos corretos da sua TV, você pode usar um receptor IR para capturar os códigos do controle remoto original.

- **Ajustes e Expansão**: Você pode adicionar mais botões e comandos conforme necessário. Para isso, você deve adicionar mais casos no `if` e ajustar os códigos IR enviados.

Esse código e esquema são um ponto de partida para criar um controle remoto de TV com Arduino. Sinta-se à vontade para adaptar e expandir o projeto conforme suas necessidades! Se precisar de ajuda com algo mais específico, é só me avisar.
