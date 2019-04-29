---
title: 使用自定义字符集发送短信
description: 使用自定义字符集发送短信
ms.assetid: c1f19c16-66f5-4bcd-ba28-950eaa6472d2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76d978497c3245c4168e9c20263f7c43fed6e6bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384647"
---
# <a name="send-sms-by-using-custom-character-sets"></a>使用自定义字符集发送短信


如果文本模式界面需要访问原始消息协议数据单元 (PDU) 来实现不支持的方案，Windows 8、 Windows 8.1 和 Windows 10 启用 PDU 模式发送和读取收到的 SMS 消息。

您可能需要使用在以下情况下的 PDU 模式 SMS 接口：

-   若要发送或通过使用单个 Shift 表的国家/地区语言或国家/地区语言锁定 Shift 表定义中读取收到的短信[3GPP TS 23.038](https://go.microsoft.com/fwlink/?LinkId=329080)。

-   若要发送多个部分组成的短信使用不同的字符集设置为每个段。

**若要使用的 PDU 模式界面发送短信的 JavaScript 代码示例**

``` syntax
function smsDevicePDUSend()
{
  if (smsDevice !== null)
  {
    // Defines a binary message
    var smsMessage = new Windows.Devices.Sms.SmsBinaryMessage();
    var messsagePdu = “0011000B914152828377F90000AA0CC8F71D14969741F977FD07”;
    var messagePduByteArray = hexToByteArray(messsagePdu);
    smsMessage.setData(messagePduByteArray);

    if (smsDevice.cellularClass === Windows.Devices.Sms.CellularClass.gsm)
    {
      smsMessage.format = Windows.Devices.Sms.SmsDataFormat.gsmSubmit;
    }
    else
    {
      smsMessage.format = Windows.Devices.Sms.SmsDataFormat.cdmaSubmit;
    }
    var sendSmsMessageOperation = smsDevice.sendMessageAsync(smsMessage);

    sendSmsMessageOperation.done(function (reply) {
      WinJS.log("Sent message in PDU format", "sample", "status");
    }, errorCallback);
}

// Used to convert hex PDU to byte array for sending SMS using PDU //mode
function hexToByteArray(hexString)
{
  var result = [];
  var hexByte = "";
  var decByte = 0;
  for (var i = 0; i < hexString.length; i = i + 2) {
    hexByte = hexString.substring(i, i + 2);
    decByte = parseInt(hexByte, 16);
    result.push(decByte);
  }
  return result;
}
```

**若要通过使用 PDU 模式界面读取收到的短信消息的 JavaScript 代码示例**

``` syntax
function smsDeviceRead()
{
  try
  {
    if (smsDevice !== null)
    {
      var messageStore = smsDevice.messageStore;
      var messageID = “1” // select a Message Id to read 

      // Check for a valid ID number
      if (isNaN(messageID) || messageID < 1 || messageID > messageStore.maxMessages)
      {
        WinJS.log("Invalid ID number", "sample", "error");
        return;
     }

     var getSmsMessageOperation = messageStore.getMessageAsync(messageID);

     // Display message when get is completed
     getSmsMessageOperation.done(smsMessageReadSuccess, errorCallback);
     } 
  }
  catch (err) {
    // handle error
  }
}

function smsMessageReadSuccess(smsMessage)
{
  try
  {
    if (smsMessage instanceof SmsBinaryMessage) {
    var format  = smsMessage.format;
    var pduData = smsMessage.getData(); // byte array 
  }
  catch (err)
  {
    WinJS.log("SMS did not set up: " + err, "sample", "error");
  }
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 SMS 应用程序](developing-sms-apps.md)

 

 






