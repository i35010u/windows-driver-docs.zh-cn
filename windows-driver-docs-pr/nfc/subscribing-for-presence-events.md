---
title: 订阅存在事件
description: 订阅存在事件
ms.assetid: 4AA6C7DA-5301-4356-8AF9-5567322FAB46
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0573820d3fe73985b237c711ce7cf06adb4d4ec6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386822"
---
# <a name="subscribing-for-presence-events"></a>订阅存在事件


存在订阅表示为驱动程序中的唯一打开句柄。 事件将引发到客户端从驱动程序每次 NFP 提供程序从过渡非近程到近程或近似为非近似。

**请注意**  此接口当前不讲述的近程设备已被删除或两个设备都大致是从哪个近程设备到达的订阅。

 

存在事件使用的典型订阅路径的实现。 协议"DeviceArrived"或"DeviceDeparted"的消息必须解释为特殊的订阅。 到达消息必须交付接收之前立即传递的第一条消息。 离开消息必须是最后一条消息后可能会没有更多消息传送。

## <a name="subscription"></a>订阅


这看起来就像常规订阅除以下特定要求。

从近似设备接收消息的协议流中涉及邻近设备和其驱动程序。

### <a name="required-actions"></a>所需的操作

该驱动程序必须接受并报告重复订阅，即使由同一客户端订阅。

-   当近程只收到第一条消息之前，该驱动程序必须其行为就好像刚刚收到虚拟"DeviceArrived"消息。
-   当提供程序转换到正在非近程驱动程序的行为必须像刚收到虚拟"DeviceDeparted"消息。
-   "DeviceDeparted"消息必须传递到客户端之前已由该客户端处理所有其他消息。
-   DeviceArrived 消息的有效负载必须是单个 DWORD 设置为零的高 31 位和最低有效位设置成为大致的第一个设备时才能够持续的双向通信。

    **请注意**  的 NFC，这相当于 LLCP 支持。

     

-   如果第一个设备成为大致是只是标记类型设备 （例如，NFC 论坛标记），该驱动程序必须清除 DeviceArrived 消息负载中的最高有效位。

     

-   DeviceDeparted 消息有效负载必须是单个 DWORD，值为 0。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

