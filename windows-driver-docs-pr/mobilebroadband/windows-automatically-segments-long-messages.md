---
title: Windows 自动将长消息分段
description: Windows 自动将长消息分段
ms.assetid: 0c1d7347-4e53-4f17-bdb5-908479f903de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb156e8c27999f69ed367eb1ef3a625fe63cb1af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377294"
---
# <a name="windows-automatically-segments-long-messages"></a>Windows 自动将长消息分段


移动宽带短信平台自动段长到基于消息内容的受支持的最大字符数限制中容纳不下的单独网段 GSM 网络发送的消息。 分段信息 （即，第 1 部分为 2） 进行编码中 SMS 用户数据标头 (UDH)，以便接收 SMS 客户端分段组合到单个消息。 通过使用相同的字符集进行编码的多个部分组成的短信的所有段。

移动网络运营商向每个消息段的用户费用。 短信平台自动创建最多 10 个段，并将截断到超出限制的文本。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用文本模式界面发送短信](send-sms-by-using-the-text-mode-interface.md)

 

 






