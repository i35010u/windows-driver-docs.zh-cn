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
ms.openlocfilehash: 3ef0f6df6271b63aaa43018f77990cf50f142b80
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381681"
---
# <a name="publishing-messages"></a>发布消息


客户端可以发布具有特定类型的消息，但会对接收该消息的人员或接收到其他应用或设备的消息的了解有一定的了解。 这样，客户端就可以轻松地将信息 "播发" 到任何感兴趣的人，无需管理消息传输时间。

Windows 近程 API 的客户端可以请求发布消息。 发布生存期将绑定到客户端。 只要客户端正在运行，它就可以维护发布。 在任何时候，客户端都可以通过取消发布)  (删除发布。 如果客户端停止运行，则会删除发布。

当某个消息被取消发布时，当某个设备将来近程时，不能再传输该消息。

NFP 模型旨在支持简短的 (，因此快速传输) 消息，通常小于512个字节。 NFP 提供程序只需要支持最大为 10 kb (KB) 的消息。 任何想要跨所有提供程序通过可移植代码发送更大消息的客户端都必须手动将消息分块或传输带外消息。

## <a name="message-transmitted-callback"></a>消息传输回调


消息传输的回叫允许客户端知道它们发布的消息是否已传输到另一台设备。 消息传输回调的目标之一就是让应用程序在传输消息后立即将其取消发布。

模型不提供接收方实际处理消息的知识。 实现此目的的唯一方法是接收方将消息发布回客户端。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)