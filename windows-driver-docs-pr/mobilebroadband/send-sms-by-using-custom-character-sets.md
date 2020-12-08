---
title: 使用自定义字符集发送短信
description: 使用自定义字符集发送短信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 188a1617cbfeae9e3545c32087e401db18f769ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821399"
---
# <a name="send-sms-by-using-custom-character-sets"></a>使用自定义字符集发送短信


如果需要访问原始消息协议数据单元 (PDU) 以实现文本模式接口、Windows 8、Windows 8.1 和 Windows 10 不支持的方案，则可以使用 PDU 模式发送和读取收到的短信。

在以下情况下，你可能需要使用 PDU 模式 SMS 接口：

-   使用国家/地区的单班次表或国家语言锁定转换表（如 [3GPP TS 23.038](https://go.microsoft.com/fwlink/?LinkId=329080)中所定义）发送或读取收到的短信。

-   为每个段使用不同的字符集发送多部分短信。

**使用 PDU 模式接口发送 SMS 消息的 JavaScript 代码示例**

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

**JavaScript 代码示例，用于通过使用 PDU 模式接口读取接收到的 SMS 消息**

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发短信应用](developing-sms-apps.md)

 

 






