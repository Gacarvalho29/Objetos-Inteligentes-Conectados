1. NODE-RED:</br>
![image](https://github.com/Gacarvalho29/Objetos-Inteligentes-Conectados/assets/85083155/5c2448da-d546-4c1f-923a-4d791e8860c8)

2. Nó 1</br>
![image](https://github.com/Gacarvalho29/Objetos-Inteligentes-Conectados/assets/85083155/03cd96be-b426-48d7-95d3-3c0dc944b5b8)

3. Nó 2</br>
![image](https://github.com/Gacarvalho29/Objetos-Inteligentes-Conectados/assets/85083155/614415b5-7381-4a2c-9db8-1df7f6ae78f8)

4. Nó 3</br>
![image](https://github.com/Gacarvalho29/Objetos-Inteligentes-Conectados/assets/85083155/09cf9fc0-1d38-4457-8819-978725152ed8)

5. Nó 4</br>
![image](https://github.com/Gacarvalho29/Objetos-Inteligentes-Conectados/assets/85083155/42052079-a9ff-4306-adc5-2ccce54b190b)

6. Nó 5</br>
![image](https://github.com/Gacarvalho29/Objetos-Inteligentes-Conectados/assets/85083155/81993237-dc4f-4f1b-b5fc-e19078e0911c)

7. Nó 6</br>
![image](https://github.com/Gacarvalho29/Objetos-Inteligentes-Conectados/assets/85083155/cb30a9ad-67ff-4255-8b1e-13491f1d9025)

8. Nó 7</br>
![image](https://github.com/Gacarvalho29/Objetos-Inteligentes-Conectados/assets/85083155/0d79056f-3f24-4ab6-91c8-7f343698437e)

9. Nó 8</br>
![image](https://github.com/Gacarvalho29/Objetos-Inteligentes-Conectados/assets/85083155/2619f8e3-6636-47cc-b7e4-695b8b4b626c)

10. Nó 9</br>
![image](https://github.com/Gacarvalho29/Objetos-Inteligentes-Conectados/assets/85083155/1faed901-8afc-466d-94b7-aa3781e7ea1f)


Código:
</br>
[
    {
        "id": "617d34943f7b1ee9",
        "type": "mqtt in",
        "z": "7c3ddfe14d3b7aca",
        "name": "",
        "topic": "TESTMACK32142293/Temperatura",
        "qos": "2",
        "datatype": "auto-detect",
        "broker": "d616c2ae350ed5f0",
        "nl": false,
        "rap": true,
        "rh": 0,
        "inputs": 0,
        "x": 360,
        "y": 180,
        "wires": [
            [
                "88061a9b8cfd5669"
            ]
        ]
    },
    {
        "id": "88061a9b8cfd5669",
        "type": "join",
        "z": "7c3ddfe14d3b7aca",
        "name": "",
        "mode": "custom",
        "build": "array",
        "property": "payload",
        "propertyType": "msg",
        "key": "payload",
        "joiner": "\\n",
        "joinerType": "str",
        "accumulate": false,
        "timeout": "",
        "count": "2",
        "reduceRight": false,
        "reduceExp": "",
        "reduceInit": "",
        "reduceInitType": "",
        "reduceFixup": "",
        "x": 650,
        "y": 280,
        "wires": [
            [
                "698407db117961f7",
                "807dc0704ba8a401",
                "dcab3fcfd8670eed"
            ]
        ]
    },
    {
        "id": "698407db117961f7",
        "type": "function",
        "z": "7c3ddfe14d3b7aca",
        "name": "function 5",
        "func": "var temp = msg.payload[0];\nvar humi = msg.payload[1];\nmsg.payload = \"A temperatura do sensor é: \" + temp + \" e a umidade do sensor é: \" + humi;\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 860,
        "y": 420,
        "wires": [
            [
                "05f9aeeaeed40401"
            ]
        ]
    },
    {
        "id": "05f9aeeaeed40401",
        "type": "node-red-contrib-whatsapp-cmb-send-message",
        "z": "7c3ddfe14d3b7aca",
        "name": "",
        "account": "eadf621fcb1b8a5d",
        "text": "payload",
        "inputtypemessage": "msg",
        "rejectssl": false,
        "x": 1040,
        "y": 420,
        "wires": [
            [
                "42b4a88761637e4d"
            ]
        ]
    },
    {
        "id": "42b4a88761637e4d",
        "type": "debug",
        "z": "7c3ddfe14d3b7aca",
        "name": "debug 4",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 1220,
        "y": 420,
        "wires": []
    },
    {
        "id": "ff1a8f1aca3ba398",
        "type": "influxdb out",
        "z": "7c3ddfe14d3b7aca",
        "influxdb": "fe8c933d5dba5ffc",
        "name": "",
        "measurement": "temp-sensor-float",
        "precision": "",
        "retentionPolicy": "",
        "database": "database",
        "precisionV18FluxV20": "ms",
        "retentionPolicyV18Flux": "",
        "org": "gabrielbco25@gmail.com",
        "bucket": "Bucket 32142293",
        "x": 1270,
        "y": 120,
        "wires": []
    },
    {
        "id": "b7504c80b67857e9",
        "type": "mqtt in",
        "z": "7c3ddfe14d3b7aca",
        "name": "",
        "topic": "TESTMACK32142293/Umidade",
        "qos": "2",
        "datatype": "auto-detect",
        "broker": "d616c2ae350ed5f0",
        "nl": false,
        "rap": true,
        "rh": 0,
        "inputs": 0,
        "x": 350,
        "y": 360,
        "wires": [
            [
                "88061a9b8cfd5669"
            ]
        ]
    },
    {
        "id": "807dc0704ba8a401",
        "type": "function",
        "z": "7c3ddfe14d3b7aca",
        "name": "function 6",
        "func": "var temp = msg.payload[0];\ntemp = parseFloat(temp)\nmsg.payload = temp;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 860,
        "y": 120,
        "wires": [
            [
                "ff1a8f1aca3ba398",
                "1735752313d8b447"
            ]
        ]
    },
    {
        "id": "e21fd568dbc02e46",
        "type": "influxdb out",
        "z": "7c3ddfe14d3b7aca",
        "influxdb": "fe8c933d5dba5ffc",
        "name": "",
        "measurement": "umi-sensor-float",
        "precision": "",
        "retentionPolicy": "",
        "database": "database",
        "precisionV18FluxV20": "ms",
        "retentionPolicyV18Flux": "",
        "org": "gabrielbco25@gmail.com",
        "bucket": "Bucket 32142293",
        "x": 1240,
        "y": 220,
        "wires": []
    },
    {
        "id": "dcab3fcfd8670eed",
        "type": "function",
        "z": "7c3ddfe14d3b7aca",
        "name": "function 7",
        "func": "var umi = msg.payload[1];\numi = parseFloat(umi);\nmsg.payload = umi;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 860,
        "y": 220,
        "wires": [
            [
                "e21fd568dbc02e46",
                "856a6c2fb6890de1"
            ]
        ]
    },
    {
        "id": "856a6c2fb6890de1",
        "type": "debug",
        "z": "7c3ddfe14d3b7aca",
        "name": "debug 5",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "statusVal": "",
        "statusType": "auto",
        "x": 1020,
        "y": 300,
        "wires": []
    },
    {
        "id": "1735752313d8b447",
        "type": "debug",
        "z": "7c3ddfe14d3b7aca",
        "name": "debug 6",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "statusVal": "",
        "statusType": "auto",
        "x": 1040,
        "y": 60,
        "wires": []
    },
    {
        "id": "d616c2ae350ed5f0",
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
        "birthTopic": "",
        "birthQos": "0",
        "birthPayload": "",
        "birthMsg": {},
        "closeTopic": "",
        "closeQos": "0",
        "closePayload": "",
        "closeMsg": {},
        "willTopic": "",
        "willQos": "0",
        "willPayload": "",
        "willMsg": {},
        "userProps": "",
        "sessionExpiry": "",
        "credentials": {}
    },
    {
        "id": "eadf621fcb1b8a5d",
        "type": "node-red-contrib-whatsapp-cmb-account",
        "name": "",
        "credentials": {}
    },
    {
        "id": "fe8c933d5dba5ffc",
        "type": "influxdb",
        "hostname": "127.0.0.1",
        "port": "8086",
        "protocol": "http",
        "database": "database",
        "name": "",
        "usetls": false,
        "tls": "",
        "influxdbVersion": "2.0",
        "url": "https://us-east-1-1.aws.cloud2.influxdata.com",
        "rejectUnauthorized": true
    }
]


