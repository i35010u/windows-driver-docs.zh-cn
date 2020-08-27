---
title: Windows 自动选择最佳字符编码
description: Windows 自动选择最佳字符编码
ms.assetid: 3fde6e89-c9ea-43d2-a999-506686b223f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d028841c6c15ee9691b101695b8c1e0e8a322ba0
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902389"
---
# <a name="windows-automatically-selects-optimal-character-encoding"></a>Windows 自动选择最佳字符编码

Windows 8、Windows 8.1 和 Windows 10 根据消息内容支持的最有效编码选择发送 SMS 消息时要使用的最佳字符编码。 SMS 以7位字符集进行编码，除非它至少包含一个无效字符，在这种情况下，将以 Unicode 编码整个消息。

## <a name="javascript-code-example-for-sending-sms-messages-using-text-mode-interface"></a>使用文本模式接口发送短信的 JavaScript 代码示例

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

还可以选择覆盖最佳编码功能，并指定要使用的字符集。

Windows 8、Windows 8.1 和 Windows 10 支持适用于与 GSM (3GPP) 和 CDMA (3GPP2) 网络兼容的移动宽带网络适配器的常见字符集。

下表列出了文本模式 API 支持的字符编码：

|网络类型|字符集|单个短信段的字符限制|多部分 SMS 段的字符限制|
|----|----|----|----|
|GSM|GSM 7 位默认字母和 GSM 7 位默认字母表扩展表|160|142|
|CDMA|7位 ASCII|160 (可能因网络) | |
|CDMA|Unicode|70 (可能因网络) | |

GSM 字符集定义 [3GPP TS 23.038： "字母和语言特定信息"](https://www.3gpp.org/DynaReport/23038.md)。 CDMA 字符集是在 [3GPP2 R1001](http://www.3gpp2.org/Public_html/specs/C.R1001-D_v1.0_110403.pdf)中定义的。

## <a name="related-topics"></a>相关主题

[使用文本模式界面读取收到的短信](read-received-sms-by-using-the-text-mode-interface.md)
