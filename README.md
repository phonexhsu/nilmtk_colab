# AIOT DS 期末專題說明

資料夾內容

- code：google colab notebook、models

- slides：期末報告投影片pdf

# Raspiberry Pi資料蒐集平台安裝步驟

## 製作Raspberry Pi SD卡映像檔
推薦使用Raspberry Pi Imager https://www.raspberrypi.com/software/
基本設定步驟請參考 [【樹莓派 Raspberry Pi】進入系統第一步設定 @ 《Four Leaf Lucky Grass》 :: 痞客邦 ::](https://tw20150525.pixnet.net/blog/post/216751866-%E3%80%90%E6%A8%B9%E8%8E%93%E6%B4%BE-raspberry-pi%E3%80%91%E9%80%B2%E5%85%A5%E7%B3%BB%E7%B5%B1%E7%AC%AC%E4%B8%80%E6%AD%A5%E8%A8%AD%E5%AE%9A)

## 安裝node-red
在raspberry pi console執行

```bash
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash - && sudo apt-get install nodejs -y && bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
```

將自動安裝nodejs 14.x的repo與package還有node-red。安裝完成後，我們需要把node-red service daemonize並啟動：

```bash
sudo systemctl enable nodered
sudo service nodered start
```

接下來我們需要安裝mongodb server，安裝把service跑起來

```bash
sudo apt install mongodb  && sudo systemctl enable mongodb && sudo service mongodb start
```

訪問http:{repasberrypi-ip}:1880就可以進到node-red的flwo editor。然後請安裝 [node-red-contrib-mongodb2 (node) - Node-RED](https://flows.nodered.org/node/node-red-contrib-mongodb2) 與 [node-red-contrib-modbus (node) - Node-RED](https://flows.nodered.org/node/node-red-contrib-modbus) 還有 https://flows.nodered.org/node/node-red-dashboard 3個packages。如何安裝package請參考 [Node-Red Palette, Importing Nodes - YouTube](https://www.youtube.com/watch?v=Wlwe5Xry5cA)。
接著請把以下的flow匯入node-red，如何匯入請參考 [Importing and Exporting Flows : Node-RED](https://nodered.org/docs/user-guide/editor/workspace/import-export)

```json
[
    {
        "id": "077af00aff80a38c",
        "type": "tab",
        "label": "流程1",
        "disabled": false,
        "info": "",
        "env": []
    },
    {
        "id": "fc4324ef.f35938",
        "type": "tab",
        "label": "relay",
        "disabled": true,
        "info": "",
        "env": []
    },
    {
        "id": "97019ae5.2c2388",
        "type": "modbus-client",
        "name": "",
        "clienttype": "simpleser",
        "bufferCommands": true,
        "stateLogEnabled": false,
        "queueLogEnabled": false,
        "tcpHost": "127.0.0.1",
        "tcpPort": "502",
        "tcpType": "DEFAULT",
        "serialPort": "/dev/ttyUSB0",
        "serialType": "RTU-BUFFERD",
        "serialBaudrate": "9600",
        "serialDatabits": "8",
        "serialStopbits": "1",
        "serialParity": "none",
        "serialConnectionDelay": "100",
        "serialAsciiResponseStartDelimiter": "",
        "unit_id": "2",
        "commandDelay": "20",
        "clientTimeout": "1000",
        "reconnectOnTimeout": true,
        "reconnectTimeout": "500",
        "parallelUnitIdsAllowed": false
    },
    {
        "id": "b9792d1f.edb0a",
        "type": "serial-port",
        "serialport": "/dev/ttyUSB0",
        "serialbaud": "9600",
        "databits": "8",
        "parity": "none",
        "stopbits": "1",
        "waitfor": "",
        "dtr": "none",
        "rts": "none",
        "cts": "none",
        "dsr": "none",
        "newline": "300",
        "bin": "bin",
        "out": "time",
        "addchar": "",
        "responsetimeout": "10000"
    },
    {
        "id": "88960d1c74c6a12e",
        "type": "ui_tab",
        "name": "Home",
        "icon": "dashboard",
        "disabled": false,
        "hidden": false
    },
    {
        "id": "4d14cc4d35c2dd6a",
        "type": "ui_base",
        "theme": {
            "name": "theme-light",
            "lightTheme": {
                "default": "#0094CE",
                "baseColor": "#0094CE",
                "baseFont": "-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen-Sans,Ubuntu,Cantarell,Helvetica Neue,sans-serif",
                "edited": true,
                "reset": false
            },
            "darkTheme": {
                "default": "#097479",
                "baseColor": "#097479",
                "baseFont": "-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen-Sans,Ubuntu,Cantarell,Helvetica Neue,sans-serif",
                "edited": false
            },
            "customTheme": {
                "name": "Untitled Theme 1",
                "default": "#4B7930",
                "baseColor": "#4B7930",
                "baseFont": "-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen-Sans,Ubuntu,Cantarell,Helvetica Neue,sans-serif"
            },
            "themeState": {
                "base-color": {
                    "default": "#0094CE",
                    "value": "#0094CE",
                    "edited": false
                },
                "page-titlebar-backgroundColor": {
                    "value": "#0094CE",
                    "edited": false
                },
                "page-backgroundColor": {
                    "value": "#fafafa",
                    "edited": false
                },
                "page-sidebar-backgroundColor": {
                    "value": "#ffffff",
                    "edited": false
                },
                "group-textColor": {
                    "value": "#1bbfff",
                    "edited": false
                },
                "group-borderColor": {
                    "value": "#ffffff",
                    "edited": false
                },
                "group-backgroundColor": {
                    "value": "#ffffff",
                    "edited": false
                },
                "widget-textColor": {
                    "value": "#111111",
                    "edited": false
                },
                "widget-backgroundColor": {
                    "value": "#0094ce",
                    "edited": false
                },
                "widget-borderColor": {
                    "value": "#ffffff",
                    "edited": false
                },
                "base-font": {
                    "value": "-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen-Sans,Ubuntu,Cantarell,Helvetica Neue,sans-serif"
                }
            },
            "angularTheme": {
                "primary": "indigo",
                "accents": "blue",
                "warn": "red",
                "background": "grey",
                "palette": "light"
            }
        },
        "site": {
            "name": "NILMTK資料搜集",
            "hideToolbar": "false",
            "allowSwipe": "false",
            "lockMenu": "false",
            "allowTempTheme": "true",
            "dateFormat": "DD/MM/YYYY",
            "sizes": {
                "sx": 48,
                "sy": 48,
                "gx": 6,
                "gy": 6,
                "cx": 6,
                "cy": 6,
                "px": 0,
                "py": 0
            }
        }
    },
    {
        "id": "b875fed7f44424f4",
        "type": "ui_group",
        "name": "用電數據報表",
        "tab": "88960d1c74c6a12e",
        "order": 2,
        "disp": true,
        "width": "6",
        "collapse": false,
        "className": ""
    },
    {
        "id": "0e399e25f6f3108c",
        "type": "mongodb2",
        "uri": "mongodb://127.0.0.1:27017",
        "name": "local db",
        "options": "",
        "parallelism": "-1"
    },
    {
        "id": "68946fb499fd9ffa",
        "type": "ui_group",
        "name": "即時用電數據",
        "tab": "88960d1c74c6a12e",
        "order": 1,
        "disp": true,
        "width": "6",
        "collapse": false,
        "className": ""
    },
    {
        "id": "2535c0a8446f23a6",
        "type": "ui_group",
        "name": "",
        "tab": "88960d1c74c6a12e",
        "order": 3,
        "disp": false,
        "width": "6",
        "collapse": false,
        "className": ""
    },
    {
        "id": "c1d5881f2ce8fc0d",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "msg.payload = msg.payload.buffer.readIntBE(0,msg.payload.buffer.length)/Math.pow(10,msg.topic.dp);\nmsg.topic = msg.topic.name;\nif (msg.topic === \"pf\") {\n    flow.set(\"theta\", Math.acos(msg.payload));\n}\nif (msg.topic === \"apparent\") {\n    msg.topic = \"reactive\";\n    msg.payload = Math.round(msg.payload * Math.sin(flow.get(\"theta\"))*100)/100;\n}\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 570,
        "y": 40,
        "wires": [
            [
                "62db514f90d16092",
                "63f488a890d3859b"
            ]
        ]
    },
    {
        "id": "8a0956c02829db54",
        "type": "inject",
        "z": "077af00aff80a38c",
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
        "repeat": "1",
        "crontab": "",
        "once": true,
        "onceDelay": 0.1,
        "topic": "",
        "payloadType": "date",
        "x": 100,
        "y": 40,
        "wires": [
            [
                "20329300edaa3f2a"
            ]
        ]
    },
    {
        "id": "20329300edaa3f2a",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "var addr = [\n    {\n        \"name\": \"voltage\",\n        \"address\": 214,\n        \"quantity\": 2,\n        \"fc\":3,\n        \"dp\":2,\n        \"unitid\":1\n    },\n    {\n        \"name\": \"current\",\n        \"address\": 216,\n        \"quantity\": 2,\n        \"fc\":3,\n        \"dp\":2,\n        \"unitid\":1\n    },\n    {\n        \"name\": \"frequency\",\n        \"address\": 218,\n        \"quantity\": 1,\n        \"fc\":3,\n        \"dp\":2,\n        \"unitid\":1\n    },\n    {\n        \"name\": \"active\",\n        \"address\": 219,\n        \"quantity\": 2,\n        \"fc\":3,\n        \"dp\":0,\n        \"unitid\":1\n    },\n    {\n        \"name\": \"pf\",\n        \"address\": 223,\n        \"quantity\": 1,\n        \"fc\":3,\n        \"dp\":2,\n        \"unitid\":1\n    },\n    {\n        \"name\": \"apparent\",\n        \"address\": 221,\n        \"quantity\": 2,\n        \"fc\":3,\n        \"dp\":0,\n        \"unitid\":1\n    }\n    ]\nfor (i=0; i<addr.length; i++) {\n    node.send({\"topic\":addr[i],\"payload\":addr[i]});\n}",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 230,
        "y": 40,
        "wires": [
            [
                "7fbf8dc3b1bc3bfa"
            ]
        ]
    },
    {
        "id": "7fbf8dc3b1bc3bfa",
        "type": "modbus-flex-getter",
        "z": "077af00aff80a38c",
        "name": "",
        "showStatusActivities": true,
        "showErrors": false,
        "logIOActivities": false,
        "server": "97019ae5.2c2388",
        "useIOFile": false,
        "ioFile": "",
        "useIOForPayload": false,
        "emptyMsgOnFail": true,
        "keepMsgProperties": true,
        "x": 400,
        "y": 40,
        "wires": [
            [],
            [
                "c1d5881f2ce8fc0d"
            ]
        ]
    },
    {
        "id": "62db514f90d16092",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "flow.set(msg.topic,msg.payload);",
        "outputs": 0,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 690,
        "y": 40,
        "wires": []
    },
    {
        "id": "aed5345658684d7c",
        "type": "inject",
        "z": "077af00aff80a38c",
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
        "repeat": "1",
        "crontab": "",
        "once": true,
        "onceDelay": "2",
        "topic": "",
        "payloadType": "date",
        "x": 100,
        "y": 220,
        "wires": [
            [
                "536e54d6e4eb94fe"
            ]
        ]
    },
    {
        "id": "536e54d6e4eb94fe",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "if (flow.get(\"start_record\") === true) return msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 230,
        "y": 220,
        "wires": [
            [
                "b33bb493c734b1e1"
            ]
        ]
    },
    {
        "id": "7492b907229fdca8",
        "type": "ui_switch",
        "z": "077af00aff80a38c",
        "name": "",
        "label": "開始記錄",
        "tooltip": "",
        "group": "b875fed7f44424f4",
        "order": 1,
        "width": 0,
        "height": 0,
        "passthru": true,
        "decouple": "false",
        "topic": "topic",
        "topicType": "msg",
        "style": "",
        "onvalue": "true",
        "onvalueType": "bool",
        "onicon": "",
        "oncolor": "",
        "offvalue": "false",
        "offvalueType": "bool",
        "officon": "",
        "offcolor": "",
        "animate": false,
        "className": "",
        "x": 240,
        "y": 100,
        "wires": [
            [
                "e8354a4546482ba1"
            ]
        ]
    },
    {
        "id": "e813fdcb01637cba",
        "type": "inject",
        "z": "077af00aff80a38c",
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
        "once": true,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "false",
        "payloadType": "bool",
        "x": 90,
        "y": 100,
        "wires": [
            [
                "7492b907229fdca8"
            ]
        ]
    },
    {
        "id": "e8354a4546482ba1",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "flow.set(\"start_record\",msg.payload);",
        "outputs": 0,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 390,
        "y": 100,
        "wires": []
    },
    {
        "id": "b33bb493c734b1e1",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "let time = new Date(msg.payload);\nmsg.payload = {\n    \"year\": time.getFullYear(),\n    \"month\": time.getMonth()+1,\n    \"date\": time.getDate(),\n    \"hour\": time.getHours(),\n    \"minute\": time.getMinutes(),\n    \"second\": time.getSeconds(),\n    \"timestamp\": msg.payload,\n    \"voltage\": flow.get(\"voltage\"),\n    \"current\": flow.get(\"current\"),\n    \"active\": flow.get(\"active\"),\n    \"reactive\": flow.get(\"reactive\"),\n    \"pf\": flow.get(\"pf\"),\n    \"frequency\": flow.get(\"frequency\")\n}\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 350,
        "y": 220,
        "wires": [
            [
                "6eec1e041934c207"
            ]
        ]
    },
    {
        "id": "720e8daa3bd68f06",
        "type": "inject",
        "z": "077af00aff80a38c",
        "name": "Timer",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "1",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payloadType": "date",
        "x": 90,
        "y": 160,
        "wires": [
            [
                "68b61a71729308f8"
            ]
        ]
    },
    {
        "id": "68b61a71729308f8",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "var d = new Date();\nlet time = {\n    \"year\": d.getFullYear(),\n    \"month\": d.getMonth()+1,\n    \"date\": d.getDate(),\n    \"hour\": d.getHours(),\n    \"minute\": d.getMinutes(),\n    \"second\": d.getSeconds(),\n    \"timestamp\": msg.payload\n};\nglobal.set(\"time\",time);",
        "outputs": 0,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 230,
        "y": 160,
        "wires": []
    },
    {
        "id": "6eec1e041934c207",
        "type": "mongodb2 in",
        "z": "077af00aff80a38c",
        "service": "_ext_",
        "configNode": "0e399e25f6f3108c",
        "name": "",
        "collection": "nilmtk",
        "operation": "insert",
        "x": 540,
        "y": 220,
        "wires": [
            []
        ]
    },
    {
        "id": "d95d574a26f4f4f8",
        "type": "ui_date_picker",
        "z": "077af00aff80a38c",
        "name": "",
        "label": "1.選擇開始日期",
        "group": "b875fed7f44424f4",
        "order": 2,
        "width": 0,
        "height": 0,
        "passthru": true,
        "topic": "topic",
        "topicType": "msg",
        "className": "",
        "x": 280,
        "y": 280,
        "wires": [
            [
                "98936dd8de0546e6"
            ]
        ]
    },
    {
        "id": "ae66329e4e622f82",
        "type": "ui_dropdown",
        "z": "077af00aff80a38c",
        "name": "",
        "label": "2.選擇輸出區間長度",
        "tooltip": "",
        "place": "",
        "group": "b875fed7f44424f4",
        "order": 3,
        "width": 0,
        "height": 0,
        "passthru": true,
        "multiple": false,
        "options": [
            {
                "label": "一日",
                "value": "day",
                "type": "str"
            },
            {
                "label": "一週",
                "value": "week",
                "type": "str"
            },
            {
                "label": "31天",
                "value": "month",
                "type": "str"
            }
        ],
        "payload": "",
        "topic": "topic",
        "topicType": "msg",
        "className": "",
        "x": 300,
        "y": 330,
        "wires": [
            [
                "78e456b1e36af44e"
            ]
        ]
    },
    {
        "id": "98936dd8de0546e6",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "flow.set(\"sdate\",msg.payload);",
        "outputs": 0,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 440,
        "y": 280,
        "wires": []
    },
    {
        "id": "78e456b1e36af44e",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "flow.set(\"duration\",msg.payload);",
        "outputs": 0,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 480,
        "y": 330,
        "wires": []
    },
    {
        "id": "e13799e5a6330ae4",
        "type": "ui_button",
        "z": "077af00aff80a38c",
        "name": "",
        "group": "b875fed7f44424f4",
        "order": 4,
        "width": 0,
        "height": 0,
        "passthru": false,
        "label": "3.產生報表",
        "tooltip": "",
        "color": "",
        "bgcolor": "",
        "className": "",
        "icon": "",
        "payload": "cp /home/pi/static/report_template.csv /home/pi/static/report.csv",
        "payloadType": "str",
        "topic": "topic",
        "topicType": "msg",
        "x": 110,
        "y": 380,
        "wires": [
            [
                "3fcd9f683e2d76dd"
            ]
        ]
    },
    {
        "id": "ce6abf34a227adac",
        "type": "inject",
        "z": "077af00aff80a38c",
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
        "once": true,
        "onceDelay": 0.1,
        "topic": "",
        "payloadType": "date",
        "x": 100,
        "y": 280,
        "wires": [
            [
                "d95d574a26f4f4f8"
            ]
        ]
    },
    {
        "id": "e968525650f7af2c",
        "type": "inject",
        "z": "077af00aff80a38c",
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
        "once": true,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "day",
        "payloadType": "str",
        "x": 90,
        "y": 330,
        "wires": [
            [
                "ae66329e4e622f82"
            ]
        ]
    },
    {
        "id": "bffe808f40e4186a",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "let date = new Date(flow.get(\"sdate\"));\nlet timestamp = new Date(date.getFullYear(),date.getMonth(),date.getDate(),0,0,0,0).getTime();\nif (flow.get(\"duration\") === \"day\") {\n    msg.payload = {\"timestamp\":{$gte:timestamp,$lt:timestamp+864000000}};\n} else if (flow.get(\"duration\") === \"week\") {\n    msg.payload = {\"timestamp\":{$gte:timestamp,$lt:timestamp+864000000*7}};\n} else if (flow.get(\"duration\") === \"month\") {\n    msg.payload = {\"timestamp\":{$gte:timestamp,$lt:timestamp+864000000*31}};\n}\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 400,
        "y": 380,
        "wires": [
            [
                "d99937593748fa20"
            ]
        ]
    },
    {
        "id": "48e3815dfd404be3",
        "type": "csv",
        "z": "077af00aff80a38c",
        "name": "",
        "sep": ",",
        "hdrin": "",
        "hdrout": "none",
        "multi": "one",
        "ret": "\\n",
        "temp": "year,month,date,hour,minute,second,timestamp,voltage,current,active,reactive,pf,frequency",
        "skip": "0",
        "strings": true,
        "include_empty_strings": "",
        "include_null_values": "",
        "x": 810,
        "y": 380,
        "wires": [
            [
                "df019ad9fdcdcf42"
            ]
        ]
    },
    {
        "id": "3fcd9f683e2d76dd",
        "type": "exec",
        "z": "077af00aff80a38c",
        "command": "",
        "addpay": "payload",
        "append": "",
        "useSpawn": "false",
        "timer": "",
        "winHide": false,
        "oldrc": false,
        "name": "",
        "x": 260,
        "y": 380,
        "wires": [
            [
                "bffe808f40e4186a"
            ],
            [],
            []
        ]
    },
    {
        "id": "df019ad9fdcdcf42",
        "type": "file",
        "z": "077af00aff80a38c",
        "name": "",
        "filename": "/home/pi/static/report.csv",
        "appendNewline": false,
        "createDir": false,
        "overwriteFile": "false",
        "encoding": "none",
        "x": 1000,
        "y": 380,
        "wires": [
            []
        ]
    },
    {
        "id": "b7ec610934168327",
        "type": "delay",
        "z": "077af00aff80a38c",
        "name": "",
        "pauseType": "delay",
        "timeout": "1",
        "timeoutUnits": "seconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "allowrate": false,
        "outputs": 1,
        "x": 950,
        "y": 430,
        "wires": [
            [
                "7b0f0dd299f6509c"
            ]
        ]
    },
    {
        "id": "2402f0387ffebe21",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "node.send({\"reset\":true});\nnode.send({\"payload\":\"報表產生完成\"});\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 810,
        "y": 430,
        "wires": [
            [
                "b7ec610934168327"
            ]
        ]
    },
    {
        "id": "7b0f0dd299f6509c",
        "type": "ui_toast",
        "z": "077af00aff80a38c",
        "position": "top right",
        "displayTime": "3",
        "highlight": "",
        "sendall": true,
        "outputs": 0,
        "ok": "OK",
        "cancel": "",
        "raw": false,
        "className": "",
        "topic": "",
        "name": "",
        "x": 1130,
        "y": 430,
        "wires": []
    },
    {
        "id": "8978b365d0d399ea",
        "type": "ui_template",
        "z": "077af00aff80a38c",
        "group": "b875fed7f44424f4",
        "name": "下載報表",
        "order": 5,
        "width": 0,
        "height": 0,
        "format": "<form method=\"get\" action=\"/report.csv\">\n    <center><button type=\"submit\">下載報表</button></center>\n</form>",
        "storeOutMessages": true,
        "fwdInMessages": true,
        "resendOnRefresh": true,
        "templateScope": "local",
        "className": "",
        "x": 100,
        "y": 440,
        "wires": [
            []
        ]
    },
    {
        "id": "d99937593748fa20",
        "type": "mongodb2 in",
        "z": "077af00aff80a38c",
        "service": "_ext_",
        "configNode": "0e399e25f6f3108c",
        "name": "",
        "collection": "nilmtk",
        "operation": "find.forEach",
        "x": 600,
        "y": 380,
        "wires": [
            [
                "48e3815dfd404be3",
                "2402f0387ffebe21"
            ]
        ]
    },
    {
        "id": "007c88459d7f5266",
        "type": "mongodb2 in",
        "z": "077af00aff80a38c",
        "service": "_ext_",
        "configNode": "0e399e25f6f3108c",
        "name": "",
        "collection": "nilmtk",
        "operation": "remove",
        "x": 1060,
        "y": 40,
        "wires": [
            []
        ]
    },
    {
        "id": "63f488a890d3859b",
        "type": "link out",
        "z": "077af00aff80a38c",
        "name": "",
        "mode": "link",
        "links": [
            "bcbe6967f217bfbf"
        ],
        "x": 655,
        "y": 80,
        "wires": []
    },
    {
        "id": "bcbe6967f217bfbf",
        "type": "link in",
        "z": "077af00aff80a38c",
        "name": "",
        "links": [
            "63f488a890d3859b"
        ],
        "x": 35,
        "y": 600,
        "wires": [
            [
                "9e887d62488bdd02",
                "8ef3f79adf31411a",
                "70e7527e31fc7eba",
                "d9ee32a4e7062f2a",
                "bcd58e24b7a1575f",
                "601cbf79c14c02be"
            ]
        ]
    },
    {
        "id": "fce1ec0d2ec0d7f2",
        "type": "ui_text",
        "z": "077af00aff80a38c",
        "group": "68946fb499fd9ffa",
        "order": 0,
        "width": 0,
        "height": 0,
        "name": "",
        "label": "電壓",
        "format": "{{msg.payload}} V",
        "layout": "row-spread",
        "className": "",
        "x": 270,
        "y": 500,
        "wires": []
    },
    {
        "id": "9e887d62488bdd02",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "if (msg.topic === \"voltage\") return msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 150,
        "y": 500,
        "wires": [
            [
                "fce1ec0d2ec0d7f2"
            ]
        ]
    },
    {
        "id": "55372aa1e4efc3b8",
        "type": "ui_text",
        "z": "077af00aff80a38c",
        "group": "68946fb499fd9ffa",
        "order": 0,
        "width": 0,
        "height": 0,
        "name": "",
        "label": "電流",
        "format": "{{msg.payload}} A",
        "layout": "row-spread",
        "className": "",
        "x": 270,
        "y": 540,
        "wires": []
    },
    {
        "id": "8ef3f79adf31411a",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "if (msg.topic === \"current\") return msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 150,
        "y": 540,
        "wires": [
            [
                "55372aa1e4efc3b8"
            ]
        ]
    },
    {
        "id": "0f2e48996f0e39df",
        "type": "ui_text",
        "z": "077af00aff80a38c",
        "group": "68946fb499fd9ffa",
        "order": 0,
        "width": 0,
        "height": 0,
        "name": "",
        "label": "有功功率",
        "format": "{{msg.payload}} W",
        "layout": "row-spread",
        "className": "",
        "x": 280,
        "y": 580,
        "wires": []
    },
    {
        "id": "70e7527e31fc7eba",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "if (msg.topic === \"active\") return msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 150,
        "y": 580,
        "wires": [
            [
                "0f2e48996f0e39df"
            ]
        ]
    },
    {
        "id": "9d4f7646e113114b",
        "type": "ui_text",
        "z": "077af00aff80a38c",
        "group": "68946fb499fd9ffa",
        "order": 0,
        "width": 0,
        "height": 0,
        "name": "",
        "label": "無效功率",
        "format": "{{msg.payload}} W",
        "layout": "row-spread",
        "className": "",
        "x": 280,
        "y": 620,
        "wires": []
    },
    {
        "id": "d9ee32a4e7062f2a",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "if (msg.topic === \"reactive\") return msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 150,
        "y": 620,
        "wires": [
            [
                "9d4f7646e113114b"
            ]
        ]
    },
    {
        "id": "3de01750bc04b241",
        "type": "ui_text",
        "z": "077af00aff80a38c",
        "group": "68946fb499fd9ffa",
        "order": 0,
        "width": 0,
        "height": 0,
        "name": "",
        "label": "功率因數",
        "format": "{{msg.payload}}",
        "layout": "row-spread",
        "className": "",
        "x": 280,
        "y": 660,
        "wires": []
    },
    {
        "id": "bcd58e24b7a1575f",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "if (msg.topic === \"pf\") return msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 150,
        "y": 660,
        "wires": [
            [
                "3de01750bc04b241"
            ]
        ]
    },
    {
        "id": "b6aa5193a7131035",
        "type": "ui_text",
        "z": "077af00aff80a38c",
        "group": "68946fb499fd9ffa",
        "order": 0,
        "width": 0,
        "height": 0,
        "name": "",
        "label": "頻率",
        "format": "{{msg.payload}} Hz",
        "layout": "row-spread",
        "className": "",
        "x": 270,
        "y": 700,
        "wires": []
    },
    {
        "id": "601cbf79c14c02be",
        "type": "function",
        "z": "077af00aff80a38c",
        "name": "",
        "func": "if (msg.topic === \"frequency\") return msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 150,
        "y": 700,
        "wires": [
            [
                "b6aa5193a7131035"
            ]
        ]
    },
    {
        "id": "767ff081eb40e6bd",
        "type": "inject",
        "z": "077af00aff80a38c",
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
        "payload": "{}",
        "payloadType": "json",
        "x": 850,
        "y": 40,
        "wires": [
            [
                "007c88459d7f5266"
            ]
        ]
    },
    {
        "id": "8b31f16dea391cc1",
        "type": "mongodb2 in",
        "z": "077af00aff80a38c",
        "service": "_ext_",
        "configNode": "0e399e25f6f3108c",
        "name": "",
        "collection": "nilmtk",
        "operation": "stats",
        "x": 1060,
        "y": 100,
        "wires": [
            [
                "a2364cabe2e665f1"
            ]
        ]
    },
    {
        "id": "fc5d355e4565190f",
        "type": "inject",
        "z": "077af00aff80a38c",
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
        "payload": "{}",
        "payloadType": "json",
        "x": 850,
        "y": 100,
        "wires": [
            [
                "8b31f16dea391cc1"
            ]
        ]
    },
    {
        "id": "a2364cabe2e665f1",
        "type": "debug",
        "z": "077af00aff80a38c",
        "name": "",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "statusVal": "",
        "statusType": "auto",
        "x": 1280,
        "y": 100,
        "wires": []
    },
    {
        "id": "84d9ccf1.6a76f",
        "type": "serial request",
        "z": "fc4324ef.f35938",
        "name": "",
        "serial": "b9792d1f.edb0a",
        "x": 420,
        "y": 380,
        "wires": [
            [
                "d709728f.8221d"
            ]
        ]
    },
    {
        "id": "fd5ea859.efee78",
        "type": "inject",
        "z": "fc4324ef.f35938",
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
        "repeat": "3",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "x": 100,
        "y": 380,
        "wires": [
            [
                "10a856d3.4d74a9",
                "e1d6b828.9833e8"
            ]
        ]
    },
    {
        "id": "10a856d3.4d74a9",
        "type": "function",
        "z": "fc4324ef.f35938",
        "name": "",
        "func": "const buf = Buffer.from([0x01, 0x03, 0x00, 0x06, 0x00, 0x09, 0x65, 0xcd]);\nmsg.payload = buf;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 260,
        "y": 380,
        "wires": [
            [
                "84d9ccf1.6a76f"
            ]
        ]
    },
    {
        "id": "3959dc07.5de6d4",
        "type": "function",
        "z": "fc4324ef.f35938",
        "name": "",
        "func": "const buf = Buffer.from([0x01, 0x03, 0x00, 0xd6, 0x00, 0x0a, 0x24, 0x35]);\nmsg.payload = buf;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 260,
        "y": 430,
        "wires": [
            [
                "ccb21bbe.d74178"
            ]
        ]
    },
    {
        "id": "ccb21bbe.d74178",
        "type": "serial request",
        "z": "fc4324ef.f35938",
        "name": "",
        "serial": "b9792d1f.edb0a",
        "x": 420,
        "y": 430,
        "wires": [
            [
                "7d200083.d7471"
            ]
        ]
    },
    {
        "id": "e1d6b828.9833e8",
        "type": "delay",
        "z": "fc4324ef.f35938",
        "name": "",
        "pauseType": "delay",
        "timeout": "0.3",
        "timeoutUnits": "seconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "outputs": 1,
        "x": 120,
        "y": 430,
        "wires": [
            [
                "3959dc07.5de6d4",
                "335e79cd.a833f6"
            ]
        ]
    },
    {
        "id": "f09859bc.0940e8",
        "type": "inject",
        "z": "fc4324ef.f35938",
        "name": "Relay on",
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
        "y": 540,
        "wires": [
            [
                "ec6809fa.6159d8"
            ]
        ]
    },
    {
        "id": "ec6809fa.6159d8",
        "type": "function",
        "z": "fc4324ef.f35938",
        "name": "",
        "func": "const buf = Buffer.from([0x01,0x16,0x8,0x8,0x0,0x2,0x4,0x1d,0x2c,0x3b,0x4a,0x20,0xb4]);\nmsg.payload = buf;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 240,
        "y": 540,
        "wires": [
            [
                "f8fe93c8.249d"
            ]
        ]
    },
    {
        "id": "f8fe93c8.249d",
        "type": "serial request",
        "z": "fc4324ef.f35938",
        "name": "",
        "serial": "b9792d1f.edb0a",
        "x": 400,
        "y": 540,
        "wires": [
            [
                "737f3ed0.5fddd"
            ]
        ]
    },
    {
        "id": "737f3ed0.5fddd",
        "type": "function",
        "z": "fc4324ef.f35938",
        "name": "",
        "func": "const buf = Buffer.from([0x01,0x10,0x00,0x49,0x00,0x01,0x02,0x00,0x01,0x69,0xc9]);\nmsg.payload = buf;\nreturn msg;\n//console.log(msg.payload === bufc);\n//if (msg.payload === bufc) {\n//    msg.payload = buf;\n//    return msg;\n//}",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 560,
        "y": 540,
        "wires": [
            [
                "d716dab9.574de8"
            ]
        ]
    },
    {
        "id": "d716dab9.574de8",
        "type": "serial request",
        "z": "fc4324ef.f35938",
        "name": "",
        "serial": "b9792d1f.edb0a",
        "x": 720,
        "y": 540,
        "wires": [
            []
        ]
    },
    {
        "id": "5c8f5b9c.833204",
        "type": "inject",
        "z": "fc4324ef.f35938",
        "name": "Relay off",
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
        "y": 580,
        "wires": [
            [
                "df339fc1.dafe3"
            ]
        ]
    },
    {
        "id": "df339fc1.dafe3",
        "type": "function",
        "z": "fc4324ef.f35938",
        "name": "",
        "func": "const buf = Buffer.from([0x01,0x16,0x8,0x8,0x0,0x2,0x4,0x1d,0x2c,0x3b,0x4a,0x20,0xb4]);\nmsg.payload = buf;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 240,
        "y": 580,
        "wires": [
            [
                "f6a122ea.44ad9"
            ]
        ]
    },
    {
        "id": "f6a122ea.44ad9",
        "type": "serial request",
        "z": "fc4324ef.f35938",
        "name": "",
        "serial": "b9792d1f.edb0a",
        "x": 400,
        "y": 580,
        "wires": [
            [
                "dcfc85ea.ff5bd8"
            ]
        ]
    },
    {
        "id": "dcfc85ea.ff5bd8",
        "type": "function",
        "z": "fc4324ef.f35938",
        "name": "",
        "func": "const buf = Buffer.from([0x01,0x10,0x00,0x49,0x00,0x01,0x02,0x00,0x02,0x29,0xc8]);\nmsg.payload = buf;\nreturn msg;\n//console.log(msg.payload === bufc);\n//if (msg.payload === bufc) {\n//    msg.payload = buf;\n//    return msg;\n//}",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 560,
        "y": 580,
        "wires": [
            [
                "ee6f2f88.76cbf"
            ]
        ]
    },
    {
        "id": "ee6f2f88.76cbf",
        "type": "serial request",
        "z": "fc4324ef.f35938",
        "name": "",
        "serial": "b9792d1f.edb0a",
        "x": 720,
        "y": 580,
        "wires": [
            []
        ]
    },
    {
        "id": "d709728f.8221d",
        "type": "function",
        "z": "fc4324ef.f35938",
        "name": "",
        "func": "node.send ({\"topic\":\"大埔國小/教室/累積度數\",\"payload\":msg.payload.readIntBE(3,4)/100});\nnode.send ({\"topic\":\"大埔國小/教室/剩餘金額\",\"payload\":msg.payload.readIntBE(11,4)/100});",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 580,
        "y": 380,
        "wires": [
            []
        ]
    },
    {
        "id": "7d200083.d7471",
        "type": "function",
        "z": "fc4324ef.f35938",
        "name": "",
        "func": "node.send ({\"topic\":\"大埔國小/教室/電壓\",\"payload\":msg.payload.readIntBE(3,4)/100});\nnode.send ({\"topic\":\"大埔國小/教室/電流\",\"payload\":msg.payload.readIntBE(7,4)/100});\nnode.send ({\"topic\":\"大埔國小/教室/頻率\",\"payload\":msg.payload.readIntBE(11,2)/100});\nnode.send ({\"topic\":\"大埔國小/教室/實功率\",\"payload\":msg.payload.readIntBE(13,4)});\nnode.send ({\"topic\":\"大埔國小/教室/視在功率\",\"payload\":msg.payload.readIntBE(17,4)});\nnode.send ({\"topic\":\"大埔國小/教室/功率因數\",\"payload\":msg.payload.readIntBE(21,2)/100});",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 580,
        "y": 430,
        "wires": [
            []
        ]
    },
    {
        "id": "335e79cd.a833f6",
        "type": "delay",
        "z": "fc4324ef.f35938",
        "name": "",
        "pauseType": "delay",
        "timeout": "0.3",
        "timeoutUnits": "seconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "outputs": 1,
        "x": 120,
        "y": 480,
        "wires": [
            [
                "6e60c002.0cc3f"
            ]
        ]
    },
    {
        "id": "6e60c002.0cc3f",
        "type": "function",
        "z": "fc4324ef.f35938",
        "name": "",
        "func": "const buf = Buffer.from([0x01, 0x03, 0x00, 0x02, 0x00, 0x01, 0x25, 0xca]);\nmsg.payload = buf;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 260,
        "y": 480,
        "wires": [
            [
                "22c5e023.29846"
            ]
        ]
    },
    {
        "id": "22c5e023.29846",
        "type": "serial request",
        "z": "fc4324ef.f35938",
        "name": "",
        "serial": "b9792d1f.edb0a",
        "x": 420,
        "y": 480,
        "wires": [
            [
                "ec345341.36762"
            ]
        ]
    },
    {
        "id": "ec345341.36762",
        "type": "function",
        "z": "fc4324ef.f35938",
        "name": "",
        "func": "msg.payload = msg.payload.readIntBE(3,2);\nif (msg.payload === 2) msg.payload = 0;\nnode.send ({\"topic\":\"大埔國小/教室/繼電器狀態\",\"payload\":msg.payload});",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 580,
        "y": 480,
        "wires": [
            []
        ]
    },
    {
        "id": "46e0c359a5fbc992",
        "type": "ui_button",
        "z": "fc4324ef.f35938",
        "name": "",
        "group": "2535c0a8446f23a6",
        "order": 0,
        "width": 0,
        "height": 0,
        "passthru": false,
        "label": "清空資料庫",
        "tooltip": "",
        "color": "",
        "bgcolor": "#ff4d4d",
        "className": "",
        "icon": "",
        "payload": "{}",
        "payloadType": "json",
        "topic": "topic",
        "topicType": "msg",
        "x": 110,
        "y": 80,
        "wires": [
            []
        ]
    }
]
```

匯入後deploy就完成資料收集平台的部署。

# NILMTK的coding實習

請參考code/nilmtk_colab.ipynb_
