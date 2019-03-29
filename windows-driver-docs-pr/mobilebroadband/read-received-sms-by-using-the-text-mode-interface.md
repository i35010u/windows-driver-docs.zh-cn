---
title: 使用文本模式界面读取收到的短信
description: 使用文本模式界面读取收到的短信
ms.assetid: 5e095fc0-59bf-4ec4-96a3-efe6f4ae054f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 640cafd6eecf72b8d19e1380389ed1f7a6bce780
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568204"
---
# <a name="read-received-sms-by-using-the-text-mode-interface"></a>使用文本模式界面读取收到的短信


您可以选择是使用文本模式下读取接口，这是适用于简单纯文本短信，或 PDU 模式模式读取接口，这是适用于解码短信的高级控制。

收到的消息存储在移动宽带设备上的编码格式。 移动宽带短信平台支持解码纯文本形式收到的消息。 支持用于解码已收到的消息的字符集不支持对于发送的消息编码的字符集相同。

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
<th>单个 SMS 段的字符数限制</th>
<th>多个部分组成的 SMS 段的字符数限制</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GSM</p></td>
<td><p>GSM 7 位默认字母表和 GSM 7 位默认字母表扩展表</p></td>
<td><p>160</p></td>
<td><p>142</p></td>
</tr>
<tr class="even">
<td><p>CDMA</p></td>
<td><p>7 位 ASCII</p></td>
<td><p>160 （可能因网络）</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>CDMA</p></td>
<td><p>Unicode</p></td>
<td><p>70 （可能因网络）</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

 

**JavaScript 代码示例读取已接收 SMS 消息使用文本模式界面**

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

**请注意**   SMS 客户端应用程序可以使用多个段的长时间消息并重新构造完整的消息的连接的 Windows 提供的已解码的细分信息。 有关已分段的 SMS 消息的详细信息，请参阅[Windows 自动段长消息](windows-automatically-segments-long-messages.md)。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 SMS 应用程序](developing-sms-apps.md)

 

 






