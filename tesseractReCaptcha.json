
[Nodered Tesseract ReCaptcha Flow]

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./src/Images/Project/nodered2.png">
  <source media="(prefers-color-scheme: light)" srcset="https://drive.google.com/file/d/1c7UXRdobbu-30hMLc89ObwgB_YxThmnK/view?usp=sharing">
  <img alt="Shows an illustrated sun in light color mode and a moon with stars in dark color mode." src="https://user-images.githubusercontent.com/25423296/163456779-a8556205-d0a5-45e2-ac17-42d089e3c3f8.png">
</picture>




[
    {
        "id": "0f5905bb3d51ccc5",
        "type": "subflow",
        "name": "İVD GİRİŞ",
        "info": "",
        "category": "",
        "in": [
            {
                "x": 40,
                "y": 140,
                "wires": [
                    {
                        "id": "826c8b87e5c06d2d"
                    }
                ]
            }
        ],
        "out": [
            {
                "x": 1300,
                "y": 300,
                "wires": [
                    {
                        "id": "e16d2c0cd119f784",
                        "port": 1
                    }
                ]
            }
        ],
        "env": [],
        "meta": {},
        "color": "#DDAA99"
    },
    {
        "id": "9b39b5f273e51294",
        "type": "http request",
        "z": "0f5905bb3d51ccc5",
        "name": "",
        "method": "GET",
        "ret": "bin",
        "paytoqs": "ignore",
        "url": "https://intvrg.gib.gov.tr/captcha/jcaptcha?imageID={{payload}}",
        "tls": "",
        "persist": false,
        "proxy": "",
        "authType": "",
        "senderr": false,
        "x": 530,
        "y": 140,
        "wires": [
            [
                "f5110bf223ac310a"
            ]
        ]
    },
    {
        "id": "3ee809ec16490611",
        "type": "function",
        "z": "0f5905bb3d51ccc5",
        "name": "",
        "func": "var dt=this.context.flow\n\n\n\n\nmsg.payload=msg.payload.replace('-','').replace('-','').slice(0,16)\n\nvar veri=dt.get(\"veri\") || msg.payload\n\n\nmsg.imageID=veri\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 360,
        "y": 140,
        "wires": [
            [
                "9b39b5f273e51294"
            ]
        ]
    },
    {
        "id": "0552b6d24b3e944b",
        "type": "function",
        "z": "0f5905bb3d51ccc5",
        "name": "",
        "func": "msg.payload=msg.payload.replace(/([\\u0300-\\u036f]|[^0-9a-zA-Z])/g, '')\n\n\nmsg.payload = \"assoscmd=multilogin&rtype=json&userid=\"+msg.user[\"gibKodu\"]+\"&sifre=\"+msg.user[\"gibSifre\"]+\"&parola=maliye&dk=\" + msg.payload + \"&imageID=\" + msg.imageID;\nmsg.headers = {};\nmsg.headers['Content-Type'] = 'application/x-www-form-urlencoded';\nmsg.headers['User-Agent'] = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.82 Safari/537.36';\n\n\n    return msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 860,
        "y": 140,
        "wires": [
            [
                "5bf18342f1d448e3"
            ]
        ]
    },
    {
        "id": "5bf18342f1d448e3",
        "type": "http request",
        "z": "0f5905bb3d51ccc5",
        "name": "",
        "method": "POST",
        "ret": "txt",
        "paytoqs": "ignore",
        "url": "https://intvrg.gib.gov.tr/intvrg_server/assos-login",
        "tls": "",
        "persist": false,
        "proxy": "",
        "authType": "",
        "senderr": false,
        "x": 1030,
        "y": 140,
        "wires": [
            [
                "e16d2c0cd119f784"
            ]
        ]
    },
    {
        "id": "e16d2c0cd119f784",
        "type": "function",
        "z": "0f5905bb3d51ccc5",
        "name": "",
        "func": "var dt=this.context.flow\n\nif(msg.payload.toString().indexOf(\"Doğrulama\")!=-1)\n{\n     \n   node.send([msg]) \n    \n}else if(msg.payload.toString().indexOf(\"token\")!=-1){\n    dt.set(\"veri\",null) \n  dt.set(\"giris\",JSON.parse(msg.payload))\n    msg.giris=JSON.parse(msg.payload)\n     msg.page=1;\n     node.send([null,msg])  \n}\nelse{\n     dt.set(\"veri\",null)\n    msg.page=1;\n  node.send([null,msg]) \n    \n}\n\n\n\n\n\n\n",
        "outputs": 2,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1140,
        "y": 240,
        "wires": [
            [
                "826c8b87e5c06d2d"
            ],
            []
        ]
    },
    {
        "id": "826c8b87e5c06d2d",
        "type": "uuid",
        "z": "0f5905bb3d51ccc5",
        "uuidVersion": "v4",
        "namespaceType": "custom",
        "namespace": "123456789",
        "namespaceCustom": "123456",
        "name": "",
        "field": "payload",
        "fieldType": "msg",
        "x": 210,
        "y": 140,
        "wires": [
            [
                "3ee809ec16490611"
            ]
        ]
    },
    {
        "id": "f5110bf223ac310a",
        "type": "tesseract",
        "z": "0f5905bb3d51ccc5",
        "name": "",
        "language": "eng",
        "x": 700,
        "y": 140,
        "wires": [
            [
                "0552b6d24b3e944b"
            ]
        ]
    }
]