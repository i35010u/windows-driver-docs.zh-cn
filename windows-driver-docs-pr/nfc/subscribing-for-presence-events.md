---
title: 订阅存在事件
description: 订阅存在事件
ms.assetid: 4AA6C7DA-5301-4356-8AF9-5567322FAB46
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54c253167bd320cd6cf1e301316d68cccfaaec6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827347"
---
# <a name="subscribing-for-presence-events"></a>订阅存在事件


出席订阅表示为驱动程序中唯一的开放句柄。 每次 NFP 提供程序从非近程转换为近程或近程转换为非近程时，驱动程序都会从驱动程序中引发一次事件。

**请注意**  此接口当前无法确定删除了哪个近程设备，或者两个设备均近程时，哪些订阅到达哪个近程设备。

 

出席事件是使用典型的订阅路径实现的。 协议为 "DeviceArrived" 或 "DeviceDeparted" 的消息必须解释为特殊订阅。 到达消息必须是在传递接收的消息之前立即传递的第一条消息。 在不能再发送消息后，出发消息必须是最后传递的消息。

## <a name="subscription"></a>订阅


除了下列特定要求以外，此类内容看起来就像常规订阅。

邻近设备及其驱动程序涉及从近程设备接收消息的协议流中。

### <a name="required-actions"></a>必需的措施

驱动程序必须接受和报告重复的订阅，即使是由同一客户端订阅。

-   紧靠近程第一条消息之前，驱动程序必须将其视为只接收了虚拟 "DeviceArrived" 消息。
-   当提供程序转换为非近程时，驱动程序必须像刚收到虚拟 "DeviceDeparted" 消息一样操作。
-   在该客户端处理所有其他消息之前，不能将 "DeviceDeparted" 消息传递给客户端。
-   DeviceArrived 消息的有效负载必须是最高31位设置为零的单个 DWORD 值和最小有效位集（仅当第一个要变为近程的设备能够持续双向通信时）。

    **请注意**，  适用于 NFC，这等同于 LLCP 支持。

     

-   如果第一个要成为近程的设备只是一个标记类型的设备（例如，NFC 论坛标记），则驱动程序必须清除 DeviceArrived 消息的负载中的最小有效位。

     

-   DeviceDeparted 消息的有效负载必须为单个 DWORD 值0。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

