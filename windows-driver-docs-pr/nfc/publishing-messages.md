---
title: 发布消息
description: 发布消息
ms.assetid: 44F8FB0B-6709-4A1C-886D-3788CA39A4D2
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6079d205c06c04cf15940a15bb4660a733a9e6f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386514"
---
# <a name="publishing-messages"></a>发布消息


客户端可以将发布与特定类型的消息，但只具有有限的知识的人员将收到以下消息，或由另一个应用或设备收到的消息。 这允许客户端轻松"播发"任何人都有兴趣而无需管理消息传输的计时信息。

Windows 邻近 API 的客户端可以请求将消息发布。 发布生存期绑定到客户端。 只要客户端正在运行，它可以维护发布。 在任何时候，客户端可以删除发布 （由取消发布）。 如果客户端将停止运行，则会删除发布。

未发布消息时它应不再传输时设备将在将来成为近似。

NFP 模型旨在支持短 （并因此快速传输） 的消息，通常不超过 512 个字节。 NFP 提供程序只需支持消息直至并包括 10 千字节 (KB)。 想要将可移植代码使用更大的消息发送到各个所有提供程序的任何客户端必须手动分块的消息或传输带外的消息。

## <a name="message-transmitted-callback"></a>消息传输回调


消息传输回调允许客户端知道何时已发布的消息已传送到另一台设备。 消息传输回调的目标之一是启用应用以取消发布一条消息，只要已传输。

该模型不提供实际用于处理消息的接收端的知识。 完成此操作的唯一方式是接收方将消息发布回客户端。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

