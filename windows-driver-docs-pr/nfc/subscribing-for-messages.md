---
title: 订阅消息
description: 订阅消息
ms.assetid: CF0D5CE0-A0E0-47D4-88E6-FBE186F78626
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17ee88d22eda73fab0228dabe904428726714edc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827353"
---
# <a name="subscribing-for-messages"></a>订阅消息


客户端可以按类型订阅消息。 接收到消息时，NFP 提供程序将仅向具有此确切类型的订阅的客户端发出消息。 接收方客户端将不知道消息的发布位置或时间，除非发布服务器将此类信息置于消息中。 模型中没有任何方法来确定还会向其他客户端发送消息。

订阅与已发布消息的生存期模型相同。

当客户端取消订阅消息时，将不再发出与取消订阅订阅类型匹配的消息。

## <a name="subscribed-message-arrival"></a>已订阅消息到达


当 NFP 提供程序收到消息时，它会将它传送到任何已订阅的客户端。 仅当订阅类型与发布的消息匹配时，才将消息传递给客户端。

模型中没有定义顺序或优先级。 提供程序可以并行发出订阅的消息，但这不是必需的。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

