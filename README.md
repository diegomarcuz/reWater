# reWater
Utilizando IOT para captar nível de água em um reservatório caseiro, como balde para incentivar o reaproveitamento de água.


## Introdução 

Nosso projeto é constituído de um reservatório caseiro, como um balde, caixa d’ água e entre outros, com um sensor de distância JSN SR-04T para captar o nível da água. Este sensor enviara a distância ao Arduino, que por sua vez utilizará o protocolo Firmata para enviar o dado do microcontrolador do Arduino até o computador, utilizado pelo proprietário. Uma vez que os dados saíram do Arduino, nós os utilizamos através da ferramenta Node-Red para poder utilizar o protocolo MQTT que envia os dados para a internet. Para que o proprietário possa se atualizar do nível da agua o mesmo pode acessar o aplicativo MQTTool. Com isso, será uma forma de automatizar o processo de reaproveitamento da água para facilitar a vida das pessoas assim incentivando cada vez mais todos a se preocuparem com o uso racional da água.

## Como reproduzir ? 

### 1. git clone: 
  - usando SSH: git@github.com:diegomarcuz/reWater.git
  - usando HTTPS: https://github.com/diegomarcuz/reWater.git

### 2. download Arduino IDE (senão possuir)
  - abrir o arquivo StandardFirmata.ino, que está dentro da pasta StandardFirmata no Arduino IDE
  - baixe a biblioteca Ultrasonic neste repositório (https://github.com/filipeflop/Ultrasonic)
  - adicione ela ao Arduino IDE, clicando em Sketch > Include library > Add .zip library
  - faz o upload para o Arduino R3 UNO usando a porta correta, de acordo com o seu sistema operacional
      - Mac: /dev/tty.usbmodem141101 (similar a isso, pode ter algumas variações, por conta de qual usb usado)
      - Windows: COM6
  
### 3. installar e executar o Node-Red
  - https://nodered.org/docs/getting-started/local
  
### 4. Ao abrir o Node-Red: 
  - Pressionar Command + I (Mac) ou CTRL + 1 (Windows) para a inserir o código JSON.
  - Abra o arquivo JSON, chamado flows_rewater.local.json (pode ser em qualquer editor de text) e cole o conteúdo dentro do       pop-up que abriu quando executou o passo a cima.
  - Uma vez copiado o JSON, clique em Import ou Importar (Aparecerá uma fluxos com varios nós)
  - Clique duas vezes no primeiro nó, chamado "String" e conecte a mesma porta mencionada do passo 2, de acordo com seu          sistema operacional, clique em Update ou Atualizar e logo em seguida Done ou Ok.
  - Clique em Deploy no canto superior direito, quando debaixo do nó chamado "String" aparecer Connected ou Conectado, a          aplicação está pronta para uso. 
  - Você poderá ver localmente um dashboard clicando em uma botao com um símbolo de gráficos no canto superior direito e então    aparece um símbolo de link externo, clique nele e abrirá uma nova aba com o dashboard. 
  
 ### 5. Execução no aplicativo:
   - Baixe o aplicativo chamado MQTTool 
   - Ao abrir este aplicativo, preencha os campos host, port e Client Id com as seguintes informações: 
      - host: broker.mqtt-dashboard.com
      - port: 1883
      - Client Id: 40ecf350-d3d4-4688-b6ea-20ec39f361bb
   - Clique em Conectar ou Connect
   - No menu apresentado na parte inferior clique em "Subscribe" 
   - Aparecerá um campo chamado topic, preencha com oic/distanciaCm
   - Clique Subscribe
   - Espera alguns segundos a distância em cm aparecerá
    
  
## Visualização do funcionamento
 - Youtube: https://youtu.be/2HcChbMOpDQ
 
## Descrição do itens utilizados
 - Sensor de distância JSN SR-04T: desenvolvido para calcular a distância com precisão de objetos entre 25cm à aproximadamente    2 metros, seu diferencial é sua resistência à umidade, sendo principalmente utilizados em ambientes úmidos, permite manter    uma grande distância do microcontrolador já que possui fio com 2.5 metros de comprimento.
 
 - Arduino R3 Uno: uma placa baseada em um microcontrolador, 14 pinos de entrada/saída digital (onde 6 podem ser usados como      saídas PWM), 6 entradas analógicas, um cristal oscilador de 16MHz, uma conexão USB, uma entrada de alimentação uma conexão    ICSP e um botão de resetentrada/saída digital.
 
 - MQTT: é um protocolo de mensagens leve que  permite aos dispositivos IoT com recursos limitados enviar ou publicar informações sobre um determinado tópico para um servidor que funciona como um mediador (broker) de mensagens MQTT.

 - 4 jumpers macho femea: tema responsabilidade de desviar, ligar ou desligar o fluxo elétrico.
 
 - Fonte chaveada 9V 1A DC Plug P4: responsável de alimentar as placas Arduino.

 - Firmata: responsável pela comunicação entre um microcontrolador e um software em um computador

 - Node-Red: é uma ferramenta de desenvolvimento baseada em fluxos para programação visual

## Documentação 
  -  define os pinos trigger 13 e echo 12 para comunicação do sensor com o arduino
  
     ![Alt text](/assets/pinos.png)

  -  responsável por incluir a biblioteca Ultrasonic para ativar o sensor JSN SR-04T
  
     ![Alt text](/assets/biblioteca.png)
     
  -  inicializa a biblioteca passando como parametro os pinos
  
     ![Alt text](/assets/ultrasonic.png)
     
  -  define após um certo tempo o envio no formato JSON, quantidade de agua já ocupado do reservatório.
  
     ![Alt text](/assets/validacao.png)

