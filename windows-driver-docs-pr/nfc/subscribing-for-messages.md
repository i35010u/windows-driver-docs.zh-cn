---
title: 订阅消息
description: 订阅消息
ms.assetid: CF0D5CE0-A0E0-47D4-88E6-FBE186F78626
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7239c3b146ca73512645473b2dc807552410725b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373623"
---
# <a name="subscribing-for-messages"></a>订阅消息


客户端可以订阅按类型对消息。 时收到消息，NFP 提供程序将仅向具有精确类型的订阅的客户端发出消息。 接收客户端将无需了解何时或何处已发布消息，除非此类信息放在消息由发布者。 没有任何用于在模型内的还确定其他哪些客户端接收消息。

订阅具有与已发布的消息相同的生命周期模型。

当客户端取消订阅的消息时它应不再颁发与取消订阅的订阅类型匹配的消息。

## <a name="subscribed-message-arrival"></a>已订阅的消息到达时


当 NFP 提供程序收到一条消息时，它会将它传送到已订阅的任何客户端。 仅当订阅类型匹配的已发布的消息时，消息将传送到客户端。

没有任何排序或在模型中定义的优先级。 它是可以接受的提供程序发出并行情况下，订阅的消息，但这不是必需。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

