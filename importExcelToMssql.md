
[Nodered Import Excel to MSSQL Flow]

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./src/Images/Project/nodered1.png">
  <source media="(prefers-color-scheme: light)" srcset="https://drive.google.com/file/d/1nAnumk1dnomtJAp9jgEqePCwxA3COdRX/view?usp=sharing">
  <img alt="Shows an illustrated sun in light color mode and a moon with stars in dark color mode." src="https://user-images.githubusercontent.com/25423296/163456779-a8556205-d0a5-45e2-ac17-42d089e3c3f8.png">
</picture>

```json

[
    {
        "id": "8e39919e4eadcf29",
        "type": "tab",
        "label": "Flow 4",
        "disabled": false,
        "info": "",
        "env": []
    },
    {
        "id": "a2e3f0459dd72d36",
        "type": "inject",
        "z": "8e39919e4eadcf29",
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
        "x": 100,
        "y": 120,
        "wires": [
            [
                "2bd74b04b28919e2"
            ]
        ]
    },
    {
        "id": "2bd74b04b28919e2",
        "type": "file in",
        "z": "8e39919e4eadcf29",
        "name": "",
        "filename": "d:\\\\kurumsal.csv",
        "format": "utf8",
        "chunk": false,
        "sendError": false,
        "encoding": "none",
        "allProps": false,
        "x": 280,
        "y": 120,
        "wires": [
            [
                "ba8a921c444fe833"
            ]
        ]
    },
    {
        "id": "ba8a921c444fe833",
        "type": "csv",
        "z": "8e39919e4eadcf29",
        "name": "",
        "sep": ";",
        "hdrin": true,
        "hdrout": "none",
        "multi": "mult",
        "ret": "\\n",
        "temp": "",
        "skip": "0",
        "strings": true,
        "include_empty_strings": false,
        "include_null_values": false,
        "x": 450,
        "y": 120,
        "wires": [
            [
                "3c44d880c860233e",
                "f2413adbc288a640"
            ]
        ]
    },
    {
        "id": "3c44d880c860233e",
        "type": "debug",
        "z": "8e39919e4eadcf29",
        "name": "",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "statusVal": "",
        "statusType": "auto",
        "x": 570,
        "y": 40,
        "wires": []
    },
    {
        "id": "f2413adbc288a640",
        "type": "function",
        "z": "8e39919e4eadcf29",
        "name": "Function",
        "func": "//node.send({\"payload\": \"insert into MQTTData (Topic,Payload) values ('\"+msg.payload[0][\"IL\"]+\"','\"+msg.payload[0][\"ILCE\"]+\"',)\"})\nvar item;\nvar data=msg.payload\n\n\nfor(item of data)\n{\n    \ntry\n{\nnode.send({\"payload\": \"insert into MQTTData (FirmaAdi,Il,Ilce) values ('\"+item[\"FIRMAADI\"]+\"','\"+item[\"IL\"]+\"','\"+item[\"ILCE\"]+\"')\"})\n}\ncatch\n{\n    \n}\n //node.send({\"topic\": \"insert into musavir (id,veri) values ('\"+item[\"GibKodu\"]+\"','\"+JSON.stringify(item)+\"')\"})\n\n}\n\n\n\n\n//??ALI??AN\n//node.send({\"payload\": \"insert into MQTTData (Topic,Payload) values ('\"+msg.payload[0][\"IL\"]+\"','\"+msg.payload[0][\"ILCE\"]+\"')\"})\n",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 640,
        "y": 120,
        "wires": [
            [
                "9c0cdb225ea79653",
                "95dfe8572d9f7a53"
            ]
        ]
    },
    {
        "id": "95dfe8572d9f7a53",
        "type": "delay",
        "z": "8e39919e4eadcf29",
        "name": "",
        "pauseType": "rate",
        "timeout": "30",
        "timeoutUnits": "seconds",
        "rate": "2",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "allowrate": false,
        "outputs": 1,
        "x": 890,
        "y": 120,
        "wires": [
            [
                "07cd5caf255407b6"
            ]
        ]
    },
    {
        "id": "9c0cdb225ea79653",
        "type": "debug",
        "z": "8e39919e4eadcf29",
        "name": "",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "statusVal": "",
        "statusType": "auto",
        "x": 810,
        "y": 40,
        "wires": []
    },
    {
        "id": "396fa0b53b8c5fbf",
        "type": "inject",
        "z": "8e39919e4eadcf29",
        "name": "Select",
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
        "onceDelay": "",
        "topic": "",
        "payload": "SELECT TOP (10) [Topic]       ,[Payload]   FROM [TestDb].[dbo].[TestTable]",
        "payloadType": "str",
        "x": 730,
        "y": 260,
        "wires": [
            [
                "07cd5caf255407b6"
            ]
        ]
    },
    {
        "id": "885d13df3807b141",
        "type": "inject",
        "z": "8e39919e4eadcf29",
        "name": "Insert",
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
        "onceDelay": "",
        "topic": "",
        "payload": "INSERT INTO [Dev].[dbo].[MQTTData] (Topic, Payload) VALUES ('msg.payload' )",
        "payloadType": "str",
        "x": 731.9999961853027,
        "y": 311.00000190734863,
        "wires": [
            [
                "07cd5caf255407b6"
            ]
        ]
    },
    {
        "id": "c939b5bf4b0f31b8",
        "type": "inject",
        "z": "8e39919e4eadcf29",
        "name": "Update",
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
        "onceDelay": "",
        "topic": "",
        "payload": "",
        "payloadType": "str",
        "x": 728.9999961853027,
        "y": 362.00000190734863,
        "wires": [
            [
                "d6dd4046e7b3ae28"
            ]
        ]
    },
    {
        "id": "be7f2d31e35c341d",
        "type": "inject",
        "z": "8e39919e4eadcf29",
        "name": "Select",
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
        "onceDelay": "",
        "topic": "",
        "payload": "2",
        "payloadType": "num",
        "x": 729.9999961853027,
        "y": 418.00000190734863,
        "wires": [
            [
                "a4c19c696b9f55f9"
            ]
        ]
    },
    {
        "id": "2943ced18214e234",
        "type": "mqtt in",
        "z": "8e39919e4eadcf29",
        "name": "",
        "topic": "SQLTest/#",
        "qos": "0",
        "datatype": "auto",
        "broker": "712b53e5.990dfc",
        "nl": false,
        "rap": false,
        "inputs": 0,
        "x": 720.9999961853027,
        "y": 468.00000190734863,
        "wires": [
            [
                "865c1585fd468a46"
            ]
        ]
    },
    {
        "id": "865c1585fd468a46",
        "type": "function",
        "z": "8e39919e4eadcf29",
        "name": "Function",
        "func": "d = new Date(),\ndformat = [d.getMonth()+1,\n    d.getDate(),\n    d.getFullYear()].join('/')+' '+\n    [d.getHours(),\n    d.getMinutes(),\n    d.getSeconds()].join(':');\n\npld =       \"INSERT INTO [Dev].[dbo].[MQTTData] \"\npld = pld + \"(Topic, Payload, Timestamp) \"\npld = pld + \"VALUES ('\" + msg.topic + \"', '\" + msg.payload + \"', '\" + dformat + \"')\"\n\nmsg.topic = ''\nmsg.payload = pld\nreturn msg;\n\n\n\n\n",
        "outputs": 1,
        "noerr": 0,
        "x": 862.9999961853027,
        "y": 468.00000190734863,
        "wires": [
            [
                "07cd5caf255407b6",
                "9f7ab5fe53f244ac"
            ]
        ]
    },
    {
        "id": "a4c19c696b9f55f9",
        "type": "function",
        "z": "8e39919e4eadcf29",
        "name": "Function",
        "func": "pld =       \"SELECT ID, Topic, Payload, Timestamp \"\npld = pld + \"FROM [Dev].[dbo].[MQTTData] \"\npld = pld + \"WHERE id = \" + msg.payload\n\nmsg.payload = pld\nreturn msg;\n\n\n\n\n",
        "outputs": 1,
        "noerr": 0,
        "x": 869.9999961853027,
        "y": 418.00000190734863,
        "wires": [
            [
                "07cd5caf255407b6"
            ]
        ]
    },
    {
        "id": "d6dd4046e7b3ae28",
        "type": "function",
        "z": "8e39919e4eadcf29",
        "name": "Function",
        "func": "d = new Date,\ndformat = [d.getMonth()+1,\n    d.getDate(),\n    d.getFullYear()].join('/')+' '+\n    [d.getHours(),\n    d.getMinutes(),\n    d.getSeconds()].join(':');\n\ndtstmp = new Date().toString();\npld =       \"UPDATE [Dev].[dbo].[MQTTData] \"\npld = pld + \"Set Timestamp = '\" + dformat + \"' \"\npld = pld + \"WHERE id = 1\"\n\nmsg.payload = pld\nreturn msg;\n\n\n\n\n",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 868.9999961853027,
        "y": 362.00000190734863,
        "wires": [
            [
                "07cd5caf255407b6"
            ]
        ]
    },
    {
        "id": "07cd5caf255407b6",
        "type": "MSSQL",
        "z": "8e39919e4eadcf29",
        "mssqlCN": "df8c0b88.91b0a8",
        "name": "MSSQL",
        "query": "",
        "outField": "payload",
        "x": 1098.9999961853027,
        "y": 246.00000190734863,
        "wires": [
            [
                "9f7ab5fe53f244ac"
            ]
        ]
    },
    {
        "id": "9f7ab5fe53f244ac",
        "type": "debug",
        "z": "8e39919e4eadcf29",
        "name": "",
        "active": true,
        "console": "false",
        "complete": "payload",
        "x": 1230,
        "y": 360,
        "wires": []
    },
    {
        "id": "712b53e5.990dfc",
        "type": "mqtt-broker",
        "name": "",
        "broker": "localhost",
        "port": "1443",
        "clientid": "NodeRedSQLClient",
        "autoConnect": true,
        "usetls": false,
        "protocolVersion": "3",
        "keepalive": "15",
        "cleansession": true,
        "birthTopic": "",
        "birthQos": "0",
        "birthPayload": "",
        "birthMsg": {},
        "closeTopic": "",
        "closePayload": "",
        "closeMsg": {},
        "willTopic": "",
        "willQos": "0",
        "willPayload": "",
        "willMsg": {},
        "sessionExpiry": ""
    },
    {
        "id": "df8c0b88.91b0a8",
        "type": "MSSQL-CN",
        "name": "TestConn",
        "server": "localhost",
        "encyption": false,
        "database": "Dev"
    }
]
```