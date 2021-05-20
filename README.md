# reWater
IOT project in order to get water level inside a homemade shell, for example a bucket in order to encourage the reuse of water.

## Video (Portuguese audio)
 - [Check here](https://elasticbeanstalk-us-east-2-596714166773.s3.us-east-2.amazonaws.com/Projeto%20de%20Objetos%20Inteligentes%20Conectados%20-%20Universidade%20Presbiteriana%20Mackenzie.mp4?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXNhLWVhc3QtMSJIMEYCIQCL6Z8t%2B4ItfuPWADldrP1aYcHPsCw1C58iCv9hEJGQ2gIhAPxzq4yd7P048gyVW5QtlXtl6%2FhECtSBxOmNNp66pqPcKv8CCIT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQARoMNTk2NzE0MTY2NzczIgySoMrgLOZmhaLdTSkq0wIDN77iPliAFAvYgIsqsmvn9nQ90iLXPw9PgXXOh4CnMU9bbnkzlJ5UpLUzMqHyAiQhtoGfLk6LWL4mzAc4lFSYhj0raN%2FoKeedzuJqp6OeBKWS7d3Bp52Z4ioJEvBl7ohSzJEpOJm8xVa%2BQspCC2WTVUULlMepAb7DJDw4iw%2FqCiUMhyk1KjyMZx56QHzrTh2qj%2BsCdmVlgrg7An342dtOZUbMVa1tTCyxUCRyiriDNh760MsrHT9YXXIZnNu%2BGAS4cXZNafn6xukmfeEXFJl%2B8YsFqn2Ch8hyZP1A1ppAOtNKD3HfTMRuch%2F7Txa3fTCG%2B6hDHwX8alWfRWLShUAiRg0DKzNshiqFRZG46QnXS94t3FJcDYVbyt4ouVfM52AP12WoVK%2B%2BVmI%2FrMnqZMl561Q1j527VrJVHG69hQGZmQaxOsrwvkVUYkXFthBWdUjaV3wwiKmXhQY6sgIJ6WyRtWl9sW9aE2D56zJZz3x5Xf5xqVm%2FcAEUqtW448If%2BV%2FhZmsxdk9BDmghhsaMMyl%2BCQm19UNnIGZ5848YDDGaedLDcf0ZCjUsQt0mM6sQKUktduErjNI1YwtfIMuYdSmMN%2FYohr8lLhingn%2BAahVqHZjqb%2B5lP0Yq9qV6CcG7Mw19wQf%2BWp7Eabc3Lh4f4%2FQFeCjfMcr8VwW7jCoGOr5aoVXMehaGYC3sh%2BQhjKQh46eYP1g8PRU3jyDWFazX3f1K%2BZ%2BGVnj%2BTDkASdilxacIcAlVjnip2KC%2BkmiOyzs6x0u0DmVNISnHTmXYRJidZa5L7owNUYh7GoD2l8kJTZhTpvYGTrRSfaxTZudogL7CwYQ3Zc49%2B52oK14zC0lq0f35xiqN3avjRT3DLSU2DuA%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20210520T031952Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAYV3XPTH23KMJKTFH%2F20210520%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=c5cef98e330cc6fed06afe82207989e4e87d11e130d0688f29c7737590c7f5ab)

## Introdução 

Nosso projeto é constituído de um reservatório caseiro, como um balde, caixa d’ água e entre outros, com um sensor de distância JSN SR-04T para captar o nível da água. Este sensor enviara a distância ao Arduino, que por sua vez utilizará o protocolo Firmata para enviar o dado do microcontrolador do Arduino até o computador, utilizado pelo proprietário. Uma vez que os dados saíram do Arduino, nós os utilizamos através da ferramenta Node-Red para poder utilizar o protocolo MQTT que envia os dados para a internet. Para que o proprietário possa se atualizar do nível da agua o mesmo pode acessar o aplicativo MQTTool. Com isso, será uma forma de automatizar o processo de reaproveitamento da água para facilitar a vida das pessoas assim incentivando cada vez mais todos a se preocuparem com o uso racional da água.

## Como reproduzir ? 

### 1. git clone: 
  - usando SSH: git@github.com:diegomarcuz/reWater.git
  - usando HTTPS: https://github.com/diegomarcuz/reWater.git

### 2. download Arduino IDE (senão possuir)
  - abrir o arquivo **StandardFirmata.ino**, que está dentro da pasta **StandardFirmata** no Arduino IDE.
  - baixe a biblioteca Ultrasonic [neste repositório](https://github.com/filipeflop/Ultrasonic).
  - adicione ela ao Arduino IDE, clicando em **Sketch** > **Include library** > **Add .zip library**.
  - faz o upload para o Arduino R3 UNO usando a porta correta, de acordo com o seu sistema operacional:
      - Mac: **/dev/tty.usbmodem141101** (similar a isso, pode ter algumas variações, por conta de qual usb usado)
      - Windows: **COM6**
  
### 3. installar e executar o Node-Red
  - [Node-Red](https://nodered.org/docs/getting-started/local).
  
### 4. Ao abrir o Node-Red: 
  - Pressionar Command + I (Mac) ou CTRL + 1 (Windows) para a inserir o código JSON.
  - Abra o arquivo JSON, chamado **flows_rewater.local.json** (pode ser em qualquer editor de text) e cole o conteúdo dentro      do pop-up que abriu quando executou o passo a cima.
  - Uma vez copiado o JSON, clique em Import ou Importar (Aparecerá uma fluxos com varios nós).
  - Clique duas vezes no primeiro nó, chamado "String" e conecte a mesma porta mencionada do **passo 2**, de acordo com seu       sistema operacional, clique em Update ou Atualizar e logo em seguida Done ou Ok.
  - Clique em Deploy no canto superior direito, quando debaixo do nó chamado "String" aparecer Connected ou Conectado, a          aplicação está pronta para uso. 
  - Você poderá ver localmente um dashboard clicando em uma botao com um símbolo de gráficos no canto superior direito e então    aparece um símbolo de link externo, clique nele e abrirá uma nova aba com o dashboard. 
  
 ### 5. Execução no aplicativo:
   - Baixe o aplicativo chamado MQTTool.
   - Ao abrir este aplicativo, preencha os campos **host**, **port** e **Client Id** com as seguintes informações: 
      - **host**: broker.mqtt-dashboard.com.
      - **port**: 1883.
      - **Client Id**: 40ecf350-d3d4-4688-b6ea-20ec39f361bb.
   - Clique em Conectar ou Connect.
   - No menu apresentado na parte inferior clique em "Subscribe".
   - Aparecerá um campo chamado topic, preencha com **oic/distanciaCm**.
   - Clique Subscribe.
   - Espera alguns segundos a distância em cm aparecerá.
    
  

 
## Descrição do itens utilizados
 - **Sensor de distância JSN SR-04T**: desenvolvido para calcular a distância com precisão de objetos entre 25cm à                aproximadamente  2 metros, seu diferencial é sua resistência à umidade, sendo principalmente utilizados em ambientes          úmidos, permite manter uma grande distância do microcontrolador já que possui fio com 2.5 metros de comprimento.
 
 - **Arduino R3 Uno**: uma placa baseada em um microcontrolador, 14 pinos de entrada/saída digital (onde 6 podem ser usados      como  saídas PWM), 6 entradas analógicas, um cristal oscilador de 16MHz, uma conexão USB, uma entrada de alimentação          uma conexão ICSP e um botão de resetentrada/saída digital.
 
 - **MQTT**: é um protocolo de mensagens leve que  permite aos dispositivos IoT com recursos limitados enviar ou publicar        informações sobre um determinado tópico para um servidor que funciona como um mediador (broker) de mensagens MQTT.

 - **4 jumpers macho femea**: tema responsabilidade de desviar, ligar ou desligar o fluxo elétrico.
 
 - **Fonte chaveada 9V 1A DC Plug P4**: responsável de alimentar as placas Arduino.

 - **Firmata**: responsável pela comunicação entre um microcontrolador e um software em um computador

 - **Node-Red**: é uma ferramenta de desenvolvimento baseada em fluxos para programação visual

## Integração 

  -  responsável por incluir a biblioteca Ultrasonic para ativar o sensor JSN SR-04T
  
~~~C++
 #include <Ultrasonic.h>
~~~

  -  define os pinos trigger 13 e echo 12 para comunicação do sensor com o arduino

~~~C++
 #define pino_trigger 13
 #define pino_echo 12
~~~

  -  inicializa a biblioteca passando como parametro os pinos
  
~~~C++
  Ultrasonic  ultrasonic(pino_trigger, pino_echo);
~~~
     
  -  A distância é recebida em segundos e transformada em centímetros. 
  
~~~C++
     long microsec = ultrasonic.timing();
     cmMsec = ultrasonic.convert(microsec, Ultrasonic::CM);
~~~
     
  - Valida se essa distância é igual a zero, se for retorna e é calculado novamente.
  
~~~C++
 if(cmMsec == 0){
        return;
  }
~~~
    
  - Faz a diferença entra a distância e o tamanho do reservatório em centímetros para obter-se o nível da água.
  
~~~C++
   qtdAguaEmCm =91 - cmMsec;
~~~
  
  - Valida se o reservatório está cheio, se estiver a distancia é igual ou maior ao tamanho do reservatório então o nível de agua é configurado para ser o tamanho do reservatório.
  
~~~C++
  if(cmMsec >= 91){
        qtdAguaEmCm = 91;
  }
~~~

  - Envia o nível da agua no formato JSON através do protocolo Firmata até o Node-red.
  
~~~C++
  Firmata.sendString((String("{\"distancia_d\":")
  +String(qtdAguaEmCm)
  +String("}")).c_str());
~~~
 
  - O Node-Red foi utilizado como plataforma de desenvolvimento para conseguir usar o protocolo de comunicação MQTT, assim que o Node-Red faz a separação dos dados para Volume (nó Transformar o cm em porcentagem) e o próprio Nível da água (nó distancia_selected), este envia para o MQTT broker
  
   <img src="/assets/node-red.png" width="600" />

  
    
  - No **nó Transformar o cm em porcentagem** ocorre a transformação para porcentagem do nível da agua baseado no tamanho do reservatório.
  
~~~javascript
var cm = msg.payload.distancia_d;
msg.payload = Math.round((cm /91)*100);
return msg;
~~~
    
  - No **nó distancia_selected** ocorre apenas a seleção do nível da água.
  
~~~javascript
msg.payload = msg.payload.distancia_d;
return msg;
~~~
  
    
  - Nos nós **oic/distanciaCm** e **oic/volumeEmPorcentagem** ocorre o envio do dados depois da transformação para o MQTT broker, respectivamente o nível da água e o volume em porcentagem.
  
  - No aplicativo MQTTool é assinado o tópico oic/distanciaCm para consultar o nível da água em centímetros.
  

    <img src="/assets/app.jpg"  width="300"/>


 ## Fluxograma
 
  ![Alt text](/assets/fluxo1.png)
  
  ![Alt text](/assets/fluxo2.png)
