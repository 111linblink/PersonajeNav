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

##Flujo de node-red
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

##Videos

https://github.com/111linblink/PersonajeNav/assets/146273461/5af57898-60a2-46a4-a69c-243528fa52c1


https://github.com/111linblink/PersonajeNav/assets/146273461/97230910-6d39-40fa-8c8c-6bbe0fb0320b


https://github.com/111linblink/PersonajeNav/assets/146273461/600e8f0b-fde9-4a97-aa90-07fd9f3f308e

##Imágenes

![image](https://github.com/111linblink/PersonajeNav/assets/146273461/74790b01-f522-4d35-bf64-791ce8e97415)

![image](https://github.com/111linblink/PersonajeNav/assets/146273461/0dbe1c3f-05c5-4bc1-9985-b0af6bfcd47a)

![image](https://github.com/111linblink/PersonajeNav/assets/146273461/de825764-8f4b-4803-9b0c-dff4ac4e74e7)

## Base de datos
![image](https://github.com/111linblink/PersonajeNav/assets/146273461/1cafe650-0457-4a22-994a-8425ddb07516)






