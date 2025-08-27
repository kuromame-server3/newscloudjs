# NEW ScloudJS

原作
[https://github.com/Frezledz/newscloudjs]
に感謝いたします。

このフォークは原作を自分が使いやすいように少し改造したものです。

### 改造点
・websocketを切断する処理を追加
   ・この機能によって定期的にログインとログアウトを繰り返すことで、接続を常時安定化することに成功

### 改造して追加した関数の使い方

```
//接続安定用のインターバル
var isS; //通信しているかのフラグ

setInterval(async () => {
  if (isS) return;
  isS = true; // 通信開始フラグ

  try {
    await scloudjs.disconnect(); // もし非同期なら await
    await func();                // 再接続処理など（下の原作のコードの例のfuncを参照）
    console.log("再接続成功");
  } catch (err) {
    console.log("再接続エラー:", err);
  } finally {
    isS = false; // 処理完了でフラグを戻す
  }
}, 60 * 2000); // 2分ごと
```

# ↓↓これより下は原作の説明

# 日本語


## システム要件
Node.js (Should be new and stable version)
## 
1. セットアップとパッケージをダウンロード
```
npm init -y
npm i scloudjs
```
2. Javascriptを使用し、いくつかのコードを作成します。

## コードの例
```
const scloudjs = require("scloudjs"); //Able to use ScloudJS as a module
let clouddatas = new Object();//Cloud variable's data will be written here
clouddatas = scloudjs.setpredata(["CLIENT","HOST_1"]);//Name of cloud datas(optional)

const process = (data)=>{//Codes you want to run when you received a message from server
   const temp = scloudjs.parsedata(data,clouddatas);//sort datas
   clouddatas = temp.clouddatas;//Cloud variable's data
   const changedlists = temp.changedlists;//List of cloud variables that has been changed
   scloudjs.sendtocloud("HOST",19);//Change value "HOST" to 19
   clouddatas["HOST"].value = 19 //Config your object because you'll not receive message when you send datas.
};

scloudjs.setdatas("username","password:","project id",process);//Config some datas

const func = async()=>{//run

    await scloudjs.login();//Login to scratch
    await scloudjs.connect();//Connect to scratch server
    await scloudjs.handshake();//connect to your project
};
func();

```
## その他
I recommend to use[ScloudJS GUI Edition](https://github.com/Frezledz/ScloudjsGUI) if you don't have enough coding skills.
## クレジット
libraries used : ws

### English


## requirements
Node.js (Should be new and stable version)
## Usage
1. Setup & Download package
```
npm init -y
npm i scloudjs
```
2. Create javascript and write a few codes

## Code examples
```
const scloudjs = require("scloudjs"); //Able to use ScloudJS as a module
let clouddatas = new Object();//Cloud variable's data will be written here
clouddatas = scloudjs.setpredata(["CLIENT","HOST_1"]);//Name of cloud datas(optional)

const process = (data)=>{//Codes you want to run when you received a message from server
   const temp = scloudjs.parsedata(data,clouddatas);//sort datas
   clouddatas = temp.clouddatas;//Cloud variable's data
   const changedlists = temp.changedlists;//List of cloud variables that has been changed
   scloudjs.sendtocloud("HOST",19);//Change value "HOST" to 19
   clouddatas["HOST"].value = 19 //Config your object because you'll not receive message when you send datas.
};

scloudjs.setdatas("username","password:","project id",process);//Config some datas

const func = async()=>{//run

    await scloudjs.login();//Login to scratch
    await scloudjs.connect();//Connect to scratch server
    await scloudjs.handshake();//connect to your project
};
func();

```
## etc
I recommend to use[ScloudJS GUI Edition](https://github.com/Frezledz/ScloudjsGUI) if you don't have enough coding skills.
## credit
libraries used : ws
