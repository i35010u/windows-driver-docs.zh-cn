---
title: 计算字符和草稿 SMS 的段
description: 计算字符和草稿 SMS 的段
ms.assetid: abbec0b0-dfa8-43e9-8b48-e99680d56b42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4d1966765bfc301892594d3f87ea859f8ba894d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541095"
---
# <a name="calculate-characters-and-segments-of-a-draft-sms"></a>计算字符和草稿 SMS 的段


移动宽带短信平台的短信组合期间提供的函数来估计的剩余字符数和使用 （在多个部分组成的消息） 段数。

**请注意**  中每个段的字符数不是常量，并根据消息正文和网络类型中的文本字符串。 GSM 网络上一条 SMS 消息支持最多 160 7 位字符或 70 的 16 位字符。 由于其他标头信息的每个段中，一条消息，跨越多个段支持 142 7 位字符。

 

提供准确的估算撰写一条短信时使用的段的数量将提升用户置信度，因为用户通常收取每个发送 SMS 消息。

**JavaScript 代码示例**

``` syntax
var smsMessage = new Windows.Devices.Sms.SmsTextMessage();
smsMessage.body = id('messageText').value;  // Set message body text to text of messageText HTML element
var messageLength = smsDevice.calculateLength(smsMessage);
id('remainingCharsCount').innerText = messageLength.charactersPerSegment - messageLength.characterCountLastSegment;
id('messageSegmentsCount').innerText = messageLength.segmentCount;
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[使用文本模式界面发送短信](send-sms-by-using-the-text-mode-interface.md)

 

 






