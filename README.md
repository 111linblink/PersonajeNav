[flows.json](https://github.com/111linblink/PersonajeNav/files/13573315/flows.json)## PersonajeNav
## Grupo
-GDS0541
## Nombre de los integrantes del equipo
 - Karen Linette Cabrera Vidal
 - Gerardo Manzano Villafaña
## Nombre del personaje
- Ángel de la guarda
## Materiales a utilizar
|Nombre del componenete|Descripción|Contidad|Precio|
|-|-|-|-|
|ESP32|Microcontrolador con 30 pines con comunicación WiFi y Bluetooth|1|$140.00|
|Cables Dupont|Cables para conexión de prototipos de pruebas|30|$30.00|
|leds|Leds para iluminar las alas del ángel|30|$50.00|
|Controlador bluetooth|para poder mandar ordenes desde el celular al personaje|1|$170.00|
|Prothoboard|Conectar los leds|1|$60.00|
|Resistencias|Medir la energía entre las conexiones|5|$10.00|
|Servomotor|	Actuador rotativo o lineal que permite lograr un control preciso en cuanto a posición angular, aceleración y velocidad del eje|1|$60.00|
|Servomotor|	Actuador rotativo o lineal que permite lograr un control preciso en cuanto a posición angular, aceleración y velocidad del eje|1|$60.00|
|Tela|Vestido del ángel|1/2m|$30.00|
|Plumas|Alas del ángel|1 bolsa|$20.00|
|Limpiapipas|Estructura para las alas de ángel|8|$15.00|
|triplay|base para los circuitos|20x20cm|$40.00|

## Software a utilizar
|Nombre|Versión|Tipo Software|
|-|-|-|
|Thonny|4.2.1|Software Libre|
|SSD1602|1.8.1|Software Libre|
|Visual Studio Code|1.8.2|Software libre|
|Wokwi||Software libre|
|Arduino IDE|2.0|Software Libre|

## Conexión en Wokwi

- Conexión
  
![image](https://github.com/111linblink/PersonajeNav/assets/146273461/fa24eb52-a8db-4aa2-ae7d-ad0fa4866116)

- Funcionaiento
  
![image](https://github.com/111linblink/PersonajeNav/assets/146273461/7ccb495a-255a-4172-ba7e-ce03ca4639d8)

- Link del archivo
  
https://wokwi.com/projects/380802798401942529

## Prototipo de dibujo
![image](https://github.com/111linblink/PersonajeNav/assets/146273461/0885c715-10f8-4bc3-a2d3-061ea24cf012)

## Comunicación
- El personaje podrá mover las alas.
- Las alas se iluminaran al ritmo de la música.
- Al momento de mover las alas de fondo se escuchará una canción navideña.
  
## Arquitectura
![image](https://github.com/111linblink/PersonajeNav/assets/146273461/b2a0c608-047a-4b04-8fc0-aa167deb2702)

## Código
#include <Stepper.h>
#include <WiFi.h>
#include <PubSubClient.h>

const char *ssid = "linksys";
const char *password = "";
const char *mqttBroker = "192.168.1.100";
const int mqttPort = 1883;
const char *mqttUser = "";
const char *mqttPassword = "";
const char *mqttClientId = "";
const char *mqttTopic = "utng/klcv/angelg";


WiFiClient espClient;
PubSubClient client(espClient);

const int stepsPerRevolution = 2048;

int DISTANCIA = 0;
int pinLed = 14;
int pinLed2 = 27;
int pinLed3 = 15;
int pinEco = 12;
int pinGatillo = 13;
int buzzer = 2;

#define IN1 19
#define IN2 18
#define IN3 5
#define IN4 17

//Notas musicales 
#define NOTE_B0  31
#define NOTE_C1  33
#define NOTE_CS1 35
#define NOTE_D1  37
#define NOTE_DS1 39
#define NOTE_E1  41
#define NOTE_F1  44
#define NOTE_FS1 46
#define NOTE_G1  49
#define NOTE_GS1 52
#define NOTE_A1  55
#define NOTE_AS1 58
#define NOTE_B1  62
#define NOTE_C2  65
#define NOTE_CS2 69
#define NOTE_D2  73
#define NOTE_DS2 78
#define NOTE_E2  82
#define NOTE_F2  87
#define NOTE_FS2 93
#define NOTE_G2  98
#define NOTE_GS2 104
#define NOTE_A2  110
#define NOTE_AS2 117
#define NOTE_B2  123
#define NOTE_C3  131
#define NOTE_CS3 139
#define NOTE_D3  147
#define NOTE_DS3 156
#define NOTE_E3  165
#define NOTE_F3  175
#define NOTE_FS3 185
#define NOTE_G3  196
#define NOTE_GS3 208
#define NOTE_A3  220
#define NOTE_AS3 233
#define NOTE_B3  247
#define NOTE_C4  262
#define NOTE_CS4 277
#define NOTE_D4  294
#define NOTE_DS4 311
#define NOTE_E4  330
#define NOTE_F4  349
#define NOTE_FS4 370
#define NOTE_G4  392
#define NOTE_GS4 415
#define NOTE_A4  440
#define NOTE_AS4 466
#define NOTE_B4  494
#define NOTE_C5  523
#define NOTE_CS5 554
#define NOTE_D5  587
#define NOTE_DS5 622
#define NOTE_E5  659
#define NOTE_F5  698
#define NOTE_FS5 740
#define NOTE_G5  784
#define NOTE_GS5 831
#define NOTE_A5  880
#define NOTE_AS5 932
#define NOTE_B5  988
#define NOTE_C6  1047
#define NOTE_CS6 1109
#define NOTE_D6  1175
#define NOTE_DS6 1245
#define NOTE_E6  1319
#define NOTE_F6  1397
#define NOTE_FS6 1480
#define NOTE_G6  1568
#define NOTE_GS6 1661
#define NOTE_A6  1760
#define NOTE_AS6 1865
#define NOTE_B6  1976
#define NOTE_C7  2093
#define NOTE_CS7 2217
#define NOTE_D7  2349
#define NOTE_DS7 2489
#define NOTE_E7  2637
#define NOTE_F7  2794
#define NOTE_FS7 2960
#define NOTE_G7  3136
#define NOTE_GS7 3322
#define NOTE_A7  3520
#define NOTE_AS7 3729
#define NOTE_B7  3951
#define NOTE_C8  4186
#define NOTE_CS8 4435
#define NOTE_D8  4699
#define NOTE_DS8 4978



// Melodía de "Santa Claus is Coming to Town"
int santa_melody[] = {
  NOTE_G4,
  NOTE_E4, NOTE_F4, NOTE_G4, NOTE_G4, NOTE_G4,
  NOTE_A4, NOTE_B4, NOTE_C5, NOTE_C5, NOTE_C5,
  NOTE_E4, NOTE_F4, NOTE_G4, NOTE_G4, NOTE_G4,
  NOTE_A4, NOTE_G4, NOTE_F4, NOTE_F4,
  NOTE_E4, NOTE_G4, NOTE_C4, NOTE_E4,
  NOTE_D4, NOTE_F4, NOTE_B3,
  NOTE_C4
};

// Duración de cada nota en milisegundos
int santa_tempo[] = {
  8,
  8, 8, 4, 4, 4,
  8, 8, 4, 4, 4,
  8, 8, 4, 4, 4,
  8, 8, 4, 2,
  4, 4, 4, 4,
  4, 2, 4,
  1
};
// We wish you a merry Christmas

int wish_melody[] = {
  NOTE_B3, 
  NOTE_F4, NOTE_F4, NOTE_G4, NOTE_F4, NOTE_E4,
  NOTE_D4, NOTE_D4, NOTE_D4,
  NOTE_G4, NOTE_G4, NOTE_A4, NOTE_G4, NOTE_F4,
  NOTE_E4, NOTE_E4, NOTE_E4,
  NOTE_A4, NOTE_A4, NOTE_B4, NOTE_A4, NOTE_G4,
  NOTE_F4, NOTE_D4, NOTE_B3, NOTE_B3,
  NOTE_D4, NOTE_G4, NOTE_E4,
  NOTE_F4
};

int wish_tempo[] = {
  4,
  4, 8, 8, 8, 8,
  4, 4, 4,
  4, 8, 8, 8, 8,
  4, 4, 4,
  4, 8, 8, 8, 8,
  4, 4, 8, 8,
  4, 4, 4,
  2
};

Stepper myStepper(stepsPerRevolution, IN1, IN3, IN2, IN4);

unsigned long previousMillis = 0;
const long interval = 100;  // Intervalo de tiempo entre cada paso del motor en milisegundos

void playMelody(int melody[], int tempo[]) {
  for (int i = 0; i < sizeof(santa_melody) / sizeof(santa_melody[0]); i++) {
    int noteDuration = 2000 / tempo[i];

    // Encender LEDs y reproducir la melodía
    digitalWrite(pinLed, HIGH);
    digitalWrite(pinLed2, HIGH);

    tone(buzzer, melody[i], noteDuration);
    delay(noteDuration * 1.1);

    // Apagar LEDs
    digitalWrite(pinLed, LOW);
    digitalWrite(pinLed2, LOW);

    noTone(buzzer);

    // Esperar un breve tiempo antes de la próxima nota
    delay(50);
  }
}

long readUltrasonicDistance(int triggerPin, int echoPin) {
  pinMode(triggerPin, OUTPUT);
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  return pulseIn(echoPin, HIGH) * 0.01723 / 2;  // Convertir a centímetros
}

void setup_wifi()
{
  delay(10);
  Serial.begin(115200);
  Serial.println();
  Serial.print("Conectando a ");
  Serial.println(ssid);

  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print(".");
  }

  Serial.println("");
  Serial.println("WiFi conectado");
  Serial.println("Dirección IP: ");
  Serial.println(WiFi.localIP());
}

void callback(char *topic, byte *payload, unsigned int length)
{
  Serial.print("Mensaje recibido en el tópico: ");
  Serial.println(topic);

  Serial.print("Contenido: ");
  for (int i = 0; i < length; i++)
  {
    Serial.print((char)payload[i]);
  }

  Serial.println();

  if (strcmp(topic, mqttTopic) == 0)
  {
    if (payload[0] == '4')
    {
      digitalWrite(pinLed3, HIGH);
      
    }
    else if (payload[0] == '5')
    {
      digitalWrite(pinLed3, LOW);
    }
    else if (payload[0] == '2')
    {
    
      myStepper.step(stepsPerRevolution);

      // Inicia la reproducción de ambas melodías al mismo tiempo
      playMelody(santa_melody, santa_tempo);
      playMelody(wish_melody, wish_tempo);
        
    }else if (payload[0] == '3')
    {
      
      noTone(buzzer);
      myStepper.step(0);
    }
    
  }
}

void reconnect()
{
  while (!client.connected())
  {
    Serial.print("Intentando conexión MQTT...");
    if (client.connect(mqttClientId, mqttUser, mqttPassword))
    {
      Serial.println("Conectado");
      client.subscribe(mqttTopic);
    }
    else
    {
      Serial.print("falló, rc=");
      Serial.print(client.state());
      Serial.println(" Intentando de nuevo en 5 segundos");
      delay(5000);
    }
  }
}

void setup() {
  Serial.begin(115200);
  setup_wifi();
  client.setServer(mqttBroker, mqttPort);
  client.setCallback(callback);

//Inicializa el stepper
  myStepper.setSpeed(7);

//
  pinMode(pinLed, OUTPUT);
  pinMode(pinLed2, OUTPUT);
  pinMode(pinLed3, OUTPUT);
}

void loop() {
  DISTANCIA = readUltrasonicDistance(pinGatillo, pinEco);
  Serial.println(DISTANCIA);

  if (DISTANCIA < 20) {
    digitalWrite(pinLed, HIGH);
    digitalWrite(pinLed2, HIGH);

    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      // Guarda el último tiempo que se ejecutó el paso del motor
      previousMillis = currentMillis;

      Serial.println("Clockwise");
      myStepper.step(stepsPerRevolution);
    }

    // Inicia la reproducción de ambas melodías al mismo tiempo
    playMelody(santa_melody, santa_tempo);
    playMelody(wish_melody, wish_tempo);
  } else {
    // Apaga los LEDs, detiene el motor y detiene la reproducción de la melodía cuando no se detecta un objeto
    digitalWrite(pinLed, LOW);
    digitalWrite(pinLed2, LOW);
    noTone(buzzer);
    myStepper.step(0);
  }

  if (!client.connected()) {
    reconnect();
  }

  client.loop();

  delay(20);
}

## Flujo de node-red
## GuardaAng
[Uploading flo[
    {
        "id": "73c3ac7f073a219d",
        "type": "tab",
        "label": "Flow 2",
        "disabled": false,
        "info": "",
        "env": []
    },
    {
        "id": "da1f32b8e584ae9f",
        "type": "ui_switch",
        "z": "73c3ac7f073a219d",
        "name": "",
        "label": "led",
        "tooltip": "",
        "group": "f3b33381b2be7e28",
        "order": 1,
        "width": 0,
        "height": 0,
        "passthru": true,
        "decouple": "false",
        "topic": "topic",
        "topicType": "msg",
        "style": "",
        "onvalue": "4",
        "onvalueType": "str",
        "onicon": "",
        "oncolor": "",
        "offvalue": "5",
        "offvalueType": "str",
        "officon": "",
        "offcolor": "",
        "animate": false,
        "className": "",
        "x": 590,
        "y": 100,
        "wires": [
            [
                "2013dd4d68a9d7bd"
            ]
        ]
    },
    {
        "id": "d77468774ecb4f7c",
        "type": "ui_switch",
        "z": "73c3ac7f073a219d",
        "name": "",
        "label": "sensor",
        "tooltip": "",
        "group": "f3b33381b2be7e28",
        "order": 2,
        "width": 0,
        "height": 0,
        "passthru": true,
        "decouple": "false",
        "topic": "topic",
        "topicType": "msg",
        "style": "",
        "onvalue": "2",
        "onvalueType": "str",
        "onicon": "",
        "oncolor": "",
        "offvalue": "3",
        "offvalueType": "str",
        "officon": "",
        "offcolor": "",
        "animate": false,
        "className": "",
        "x": 590,
        "y": 260,
        "wires": [
            [
                "2013dd4d68a9d7bd"
            ]
        ]
    },
    {
        "id": "2013dd4d68a9d7bd",
        "type": "mqtt out",
        "z": "73c3ac7f073a219d",
        "name": "",
        "topic": "utng/klcv/led",
        "qos": "2",
        "retain": "",
        "respTopic": "",
        "contentType": "",
        "userProps": "",
        "correl": "",
        "expiry": "",
        "broker": "1c48427011033ec0",
        "x": 850,
        "y": 180,
        "wires": []
    },
    {
        "id": "c3fa15d06271d1ca",
        "type": "inject",
        "z": "73c3ac7f073a219d",
        "name": "",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "x": 340,
        "y": 200,
        "wires": [
            [
                "da1f32b8e584ae9f",
                "d77468774ecb4f7c"
            ]
        ]
    },
    {
        "id": "6323180c90194674",
        "type": "debug",
        "z": "73c3ac7f073a219d",
        "name": "debug 1",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "statusVal": "",
        "statusType": "auto",
        "x": 840,
        "y": 80,
        "wires": []
    },
    {
        "id": "f3b33381b2be7e28",
        "type": "ui_group",
        "name": "Controles",
        "tab": "130465b46c2f9d58",
        "order": 1,
        "disp": true,
        "width": "6",
        "collapse": false,
        "className": ""
    },
    {
        "id": "1c48427011033ec0",
        "type": "mqtt-broker",
        "name": "",
        "broker": "broker.hivemq.com",
        "port": "1883",
        "clientid": "",
        "autoConnect": true,
        "usetls": false,
        "protocolVersion": "4",
        "keepalive": "60",
        "cleansession": true,
        "autoUnsubscribe": true,
        "birthTopic": "",
        "birthQos": "0",
        "birthRetain": "false",
        "birthPayload": "",
        "birthMsg": {},
        "closeTopic": "",
        "closeQos": "0",
        "closeRetain": "false",
        "closePayload": "",
        "closeMsg": {},
        "willTopic": "",
        "willQos": "0",
        "willRetain": "false",
        "willPayload": "",
        "willMsg": {},
        "userProps": "",
        "sessionExpiry": ""
    },
    {
        "id": "130465b46c2f9d58",
        "type": "ui_tab",
        "name": "Ángel",
        "icon": "dashboard",
        "order": 1,
        "disabled": false,
        "hidden": false
    }
]ws.json…]()

## Videos

https://github.com/111linblink/PersonajeNav/assets/146273461/5af57898-60a2-46a4-a69c-243528fa52c1


https://github.com/111linblink/PersonajeNav/assets/146273461/97230910-6d39-40fa-8c8c-6bbe0fb0320b


https://github.com/111linblink/PersonajeNav/assets/146273461/600e8f0b-fde9-4a97-aa90-07fd9f3f308e

## Imágenes

![image](https://github.com/111linblink/PersonajeNav/assets/146273461/74790b01-f522-4d35-bf64-791ce8e97415)

![image](https://github.com/111linblink/PersonajeNav/assets/146273461/0dbe1c3f-05c5-4bc1-9985-b0af6bfcd47a)

![image](https://github.com/111linblink/PersonajeNav/assets/146273461/de825764-8f4b-4803-9b0c-dff4ac4e74e7)

## Base de datos
![image](https://github.com/111linblink/PersonajeNav/assets/146273461/1cafe650-0457-4a22-994a-8425ddb07516)






