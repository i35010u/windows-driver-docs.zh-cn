---
title: 消息传输
description: 消息传输
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 659c887227d19bc75f64cd03e3bbdcc1bf631e24
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97090804"
---
# <a name="message-transmission"></a>消息传输


当 NFP 技术确定另一个设备近程（如近程技术定义）时，这应充当在设备之间传输已发布消息的触发器。

在设备处于邻近范围内时，已发布的消息只应传输一次。

每次设备进入邻近范围时，都应传输所有当前已发布的消息。

如果在近程设备时发布消息，而触发器仍处于活动状态，则应传输该消息。

将发布传递到近程设备并不意味着该发布应由 NFP 提供程序取消发布。 对于下一个近程事件，发布保持活动状态，直到客户端 unpublishes。

NFP 设备驱动程序接口不要求按发布的消息发布的顺序进行传输。 NFP 设备驱动程序接口不需要将所有发布的消息作为单个块传输。 NFC 专门提供了一些详细的互操作要求，可防止出现这种情况：不允许将多个消息作为单个块传输。 但是，要求完全接收并不出错的单个已发布消息，否则不应将这些消息传递给订阅的客户端。

如果接收设备上的任何应用订阅了消息，则在 NFP 设备驱动程序接口中未定义任何机制来通知客户端。 还没有用于告诉客户端收到的消息未订阅的机制。

 

 
## <a name="related-topics"></a>相关主题
[近现场通信 (NFC) API 参考](/windows-hardware/drivers/ddi/_nfpdrivers/)
