---
title: 使用文本模式界面读取收到的短信
description: 使用文本模式界面读取收到的短信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1df8a55532c24171696e1c631b12645314fd40ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782301"
---
# <a name="read-received-sms-by-using-the-text-mode-interface"></a>使用文本模式界面读取收到的短信


你可以选择使用文本模式读取界面，该界面适用于简单的纯文本短信，或 PDU 模式的 "读取接口"，它适用于对 SMS 消息解码的高级控制。

在移动宽带设备上以编码格式存储接收的消息。 移动宽带 SMS 平台支持将收到的消息解码为纯文本。 支持对接收的消息进行解码的字符集与发送的编码消息所支持的字符集相同。

下表列出了文本模式 API 支持的字符编码：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>网络类型</th>
<th>字符集</th>
<th>单个短信段的字符限制</th>
<th>多部分 SMS 段的字符限制</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GSM</p></td>
<td><p>GSM 7 位默认字母和 GSM 7 位默认字母表扩展表</p></td>
<td><p>160</p></td>
<td><p>142</p></td>
</tr>
<tr class="even">
<td><p>CDMA</p></td>
<td><p>7位 ASCII</p></td>
<td><p>160 (可能因网络) </p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>CDMA</p></td>
<td><p>Unicode</p></td>
<td><p>70 (可能因网络) </p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

 

**用于读取使用文本模式接口接收到的 SMS 消息的 JavaScript 代码示例**

``` syntax
try
{
  if (smsDevice!= null)
  {
    var messageStore = smsDevice.messageStore;
    var messageID = id('whichMessage').value;

    var getSmsMessageOperation = messageStore.getMessageAsync(messageID);

    getSmsMessageOperation.operation.completed = function ()
    {
      result = getSmsMessageOperation.operation.getResults();
      var readableMessage = new Windows.Devices.Sms.SmsTextMessage.fromBinaryMessage(result);
      id('fromWho').innerHTML = readableMessage.from;
      id('fromMessageBody').innerHTML = readableMessage.body;
      console.log("Successfully retrieved message " + messageID + " from message store.");
    }
    getSmsMessageOperation.operation.start();
  }
  else 
  {
    console.log("No SMS Device Found");
  }
}
catch (err) 
{
  console.log("SMS did not set up: " + err);
}
```

**注意**  
SMS 客户端应用程序可以使用 Windows 提供的已解码分段信息连接长消息的多个段，并重新构造完整的消息。 有关分段短信消息的详细信息，请参阅 [Windows 自动段长消息](windows-automatically-segments-long-messages.md)。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发短信应用](developing-sms-apps.md)

 

 






