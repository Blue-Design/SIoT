# siot：让MQTT更加好用

## 简介

SIoT是一款开源的MQTT服务器（代理），siot则是Python和MicroPython的一个库。

## 开发说明

MQTT的库明显不好用，前面要定义一个类，代码还很长，让初学者紧张。

siot是虚谷物联团队写的一个Python库。为了让初学者能够写出更加简洁、优雅的Python代码。

siot库同时支持MicroPython，语法完全一致。

## 安装

使用pip命令安装。

pip3 install siot

pip install siot

当权限不够时需要使用sudo

sudo pip3 install siot

sudo pip install siot

## 官方地址

- GitHub地址：https://github.com/vvlink/SIoT/tree/master/siot-lib

## 使用说明：

### 代码范例：

- 发送消息：

```
import siot
import time

SERVER = "127.0.0.1"            #MQTT服务器IP
CLIENT_ID = ""                  #在SIoT上，CLIENT_ID可以留空
IOT_pubTopic  = 'xzr/001'       #“topic”为“项目名称/设备名称”
IOT_UserName ='siot'            #用户名
IOT_PassWord ='dfrobot'         #密码

siot.init(CLIENT_ID, SERVER, user=IOT_UserName, password=IOT_PassWord)
siot.connect()
siot.loop()

tick = 0

try:
    while True:
        siot.publish(IOT_pubTopic, "value %d"%tick)
        time.sleep(1)           #隔1秒发送一次
        tick = tick+1
except:
    siot.stop()
    print("disconnect seccused")
```

- 订阅消息：

```
import siot
import time

SERVER = "127.0.0.1"        #MQTT服务器IP
CLIENT_ID = ""              #在SIoT上，CLIENT_ID可以留空
IOT_pubTopic  = 'xzr/001'   #“topic”为“项目名称/设备名称”
IOT_UserName ='siot'        #用户名
IOT_PassWord ='dfrobot'     #密码

def sub_cb(client, userdata, msg):
  print("\nTopic:" + str(msg.topic) + " Message:" + str(msg.payload))

siot.init(CLIENT_ID, SERVER, user=IOT_UserName, password=IOT_PassWord)
siot.connect()
siot.subscribe(IOT_pubTopic, sub_cb)
siot.loop()

try:
  while True:
    pass
except:
  siot.stop()
  print("disconnect seccused")
```
