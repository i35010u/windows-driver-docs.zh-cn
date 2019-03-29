---
title: Windows 自动选择最佳字符编码
description: Windows 自动选择最佳字符编码
ms.assetid: 3fde6e89-c9ea-43d2-a999-506686b223f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88e21083fe59d46ee4c9fae0e285f67e7b2db7a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566498"
---
# <a name="windows-automatically-selects-optimal-character-encoding"></a>Windows 自动选择最佳字符编码


Windows 8、 Windows 8.1 和 Windows 10 选择的最佳字符编码时发送短信，最高效编码支持的消息内容的基础使用。 SMS 编码中的 7 位字符，除非它包含至少一个无效的字符，以 Unicode 编码用例的整个消息。

**发送 SMS 消息使用文本模式界面的 JavaScript 代码示例**

``` syntax
try
{
    if (smsDevice != null)
    {
      // defines a text message
      var smsMessage = new Windows.Devices.Sms.SmsTextMessage();
      smsMessage.to = id("phoneNumber").value;
      smsMessage.body = id("messageText").value + "\n\nSent via Windows 8 SMS API";
      var sendSmsMessageOperation = smsDevice.sendMessageAsync(smsMessage);
      console.log("Sending message...");
      sendSmsMessageOperation.then(function (reply)
      {
        console.log("Text message sent.");
      });
    }
    else
    {
      console.log("No SMS device found");
    }
} catch (err) {
    console.log("SMS exception: " + err);
}
```

（可选） 可以重写最佳的编码功能，并指定要使用哪个字符集。

Windows 8、 Windows 8.1 和 Windows 10 支持的常见字符设置与 GSM (3GPP) 和 CDMA (3GPP2) 网络兼容的移动宽带网络适配器。

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

 

定义 GSM 字符集[3GPP TS 23.038:"字母和特定于语言的信息"](http://www.3gpp.org/ftp/Specs/html-info/23038.md)。 在中定义 CDMA 字符集[3GPP2 C.R1001-D](http://www.3gpp2.org/Public_html/specs/C.R1001-D_v1.0_110403.pdf)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用文本模式界面发送短信](send-sms-by-using-the-text-mode-interface.md)

 

 






