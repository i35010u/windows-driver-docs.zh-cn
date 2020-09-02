---
title: Windows 自动将长消息分段
description: Windows 自动将长消息分段
ms.assetid: 0c1d7347-4e53-4f17-bdb5-908479f903de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5a81b35959dc89baf4189e28676fb23227769d2
ms.sourcegitcommit: 7e4d9508198a30bdc1cb6eda83852dda4e42213e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304278"
---
# <a name="windows-automatically-segments-long-messages"></a>Windows 自动将长消息分段


移动宽带 SMS 平台会自动将 GSM 网络上发送的长消息分割为单独的段，这些段根据消息内容所支持的最大字符数限制。 分段信息 (也就是说，第1部分（共2个) ）在 SMS 用户数据标头 (UDH) 中进行编码，以便接收 SMS 客户端将段合并为单个消息。 多部分 SMS 的所有段都使用同一字符集进行编码。

移动网络操作员按消息段向用户收费。 SMS 平台会自动创建最多10个段，并且截断超出限制的文本。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用文本模式界面发送短信](calculate-characters-and-segments-of-a-draft-sms.md)

 

 






