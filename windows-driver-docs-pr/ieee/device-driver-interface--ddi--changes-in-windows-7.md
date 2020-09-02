---
title: Windows 7 中的设备驱动程序接口 (DDI) 更改
description: 本主题概述了支持新的1394总线驱动程序的常规 DDI 更改。
ms.assetid: 5473C6AC-284C-41B1-AA67-75696BE96C24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6150ae340c05132a0fd37a040286093694445e0f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382249"
---
# <a name="device-driver-interface-ddi-changes-in-windows-7"></a>Windows 7 中的设备驱动程序接口 (DDI) 更改

Windows 7 包括 1394ohci.sys，这是通过使用内核模式驱动程序框架（ (KMDF) 实现的新 IEEE 1394 总线驱动程序）。 新的1394总线驱动程序替换端口/微型端口 configuration--1394bus.sys 和 ochi1394.sys 中的旧 IEEE 总线驱动程序。 新的 DDIs 已添加到 1394ohci.sys 支持的新功能中。 此外，某些 1394 DDIs 已更改为支持1394b 规范定义的更多速度，并经过改进，简化了1394客户端驱动程序的开发。

本主题概述了支持新的1394总线驱动程序的常规 DDI 更改。

* [扩展总线重置通知](#extended-bus-reset-notification)
* [用于 PHY 数据包支持的新 IOCTLs](#new-ioctls-for-phy-packet-support)
* [用于检索配置 ROM 的新 IOCTL](#new-ioctl-to-retrieve-configuration-rom)
* [IEEE Bus 驱动程序 DDI 更改](#ieee-bus-driver-ddi-changes)
* [速度和负载大小的新标志](#new-flags-for-speed-and-payload-size)
* [IEEE 1394 IOCTL 更改](#ieee-1394-ioctl-changes)
* [相关主题](#related-topics)

## <a name="extended-bus-reset-notification"></a>扩展总线重置通知

1394ohci.sys 总线驱动程序支持扩展总线重置通知。 此通知返回有关当前生成的总线 (的信息，例如，在总线重置通知上下文中) 到1394客户端驱动程序的生成计数和节点 id。 利用此信息，无需使用1394客户端驱动程序，就可以使用其总线重置通知处理程序来同步对生成计数、节点 id 和其他信息的检索。

若要注册扩展总线重置通知，客户端驱动程序使用现有 [**请求 \_ 总线 \_ 重置 \_ 通知**](https://msdn.microsoft.com/library/windows/hardware/ff537638) I/o 请求，并 \_ \_ 在 **BUSRESETNOTIFICATION. fulFlags** 参数中指定新的扩展通知例程标志。 \_指定扩展通知 \_ 例程标志后， **BusResetNotification. ResetContext**参数指向[**总线 \_ 重置 \_ 数据**](/windows-hardware/drivers/ddi/1394/ns-1394-_bus_reset_data)结构。

## <a name="new-ioctls-for-phy-packet-support"></a>用于 PHY 数据包支持的新 IOCTLs

1394ohci.sys 总线驱动程序公开了以下新 DDIs，用于发送和接收 PHY 数据包，如 IEEE-1394a 规范中所定义。

* [**请求 \_ 发送 \_ PHY \_ 数据包**](https://msdn.microsoft.com/library/windows/hardware/gg266407)
* [**请求 \_ 接收 \_ PHY \_ 数据包**](https://msdn.microsoft.com/library/windows/hardware/gg266406)

应使用新 [**请求 \_ 发送 \_ phy \_ 数据包**](https://msdn.microsoft.com/library/windows/hardware/gg266407) i/o 请求，而不是 [**请求 \_ 发送 \_ phy \_ 配置 \_ 数据包**](https://msdn.microsoft.com/library/windows/hardware/ff537661)。 后一 i/o 请求不允许指定生成计数，这可能会导致将 PHY 数据包发送到错误的1394总线生成。

## <a name="new-ioctl-to-retrieve-configuration-rom"></a>用于检索配置 ROM 的新 IOCTL

新的 IOCTL、 [**请求 \_ 获取 \_ 配置 \_ ROM**](https://msdn.microsoft.com/library/windows/hardware/gg266404)返回节点配置 rom 的内容，最大大小为 1 kb (KB) 。 1394ohci.sys 总线驱动程序仅支持 1 KB 配置 Rom，这与旧版1394总线驱动程序相同。

## <a name="ieee-bus-driver-ddi-changes"></a>IEEE Bus 驱动程序 DDI 更改

下表描述了新1394总线驱动程序公开的 DDIs 的功能行为更改和旧1394总线驱动程序：

| 设备驱动程序接口                                                              | 说明                                                                                                                                                                                                                                                                          |
|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**请求 \_ 获取 \_ 本地 \_ 主机 \_ 信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644)             | 1394ohci.sys 总线驱动程序不支持将 **nLevel** 设置为获取 \_ 主机 \_ CSR \_ 内容并将速度 \_ 映射位置指定 \_ 为 **CsrBaseAddress**。 速度图在 IEEE-1394a 规范中已过时。                                                                |
| [**请求 \_ 获取 \_ 速度 \_ 拓扑 \_ 图**](https://msdn.microsoft.com/library/windows/hardware/ff537646)     | [**请求 \_Windows 2000 和更高版本的操作系统中已弃用获取 \_ 速度 \_ 拓扑 \_ 图**](https://msdn.microsoft.com/library/windows/hardware/ff537646) 。 将此请求发送到 1394ohci.sys 返回状态 \_ 无效 \_ 参数。                                            |
| [**请求 \_ \_ \_ 在设备之间获取速度 \_**](https://msdn.microsoft.com/library/windows/hardware/ff537645) | 发送 [**请求在 \_ \_ 设备请求 \_ 之间 \_ 获取速度**](https://msdn.microsoft.com/library/windows/hardware/ff537645) 1394ohci.sys 检索本地节点与设备之间的速度。 \_ \_ 必须在**GetMaxSpeedBetweenDevices. fulFlags**参数中设置 "使用本地节点" 标志。 |

## <a name="new-flags-for-speed-and-payload-size"></a>速度和负载大小的新标志

Windows 7 Windows 驱动程序工具包中的1394头文件（即 1394 .h）定义了新标志以提高速度和提高负载。 本部分介绍这些新的标志和值。

下表描述了每个新支持的速度的最大异步负载大小。

| 标志                       | 值 | 说明 |
|----------------------------|-------|-------------|
| ASYNC \_ 负载 \_ 800 \_ 速率  | 4096  | 800 Mb/秒    |
| ASYNC \_ 负载 \_ 1600 \_ 速率 | 4096  | 160 Mb/秒    |
| ASYNC \_ 负载 \_ 3200 \_ 速率 | 4096  | 3200 Mb/秒   |

下表描述了每个新支持的速度的速度标志。

| 标志               | 值 | 说明 |
|--------------------|-------|-------------|
| 速度 \_ 标志 \_ 800  | 0x08  | 800 Mb/秒    |
| 速度 \_ 标志 \_ 1600 | 0x10  | 160 Mb/秒    |
| 速度 \_ 标志 \_ 3200 | 0x20  | 3200 Mb/秒   |

下表描述了每个新支持的速度的速度代码值。

| 标志              | 值 | 说明 |
|-------------------|-------|-------------|
| SCODE \_ 800 \_ 速率  | 3     | 800 Mb/秒    |
| SCODE \_ 1600 \_ 速率 | 4     | 160 Mb/秒    |
| SCODE \_ 3200 \_ 速率 | 5     | 3200 Mb/秒   |

## <a name="ieee-1394-ioctl-changes"></a>IEEE 1394 IOCTL 更改

本部分介绍使用新速度和有效负载大小值的 1394 i/o 请求。

[**请求 \_ 异步 \_ 读取**](https://msdn.microsoft.com/library/windows/hardware/ff537634)  
**AsyncRead. nBlockSize**

指定数据流中从1394节点读取的每个块的大小。 如果此参数为零，则将使用所选设备的最大数据包大小和所选的速度来发出这些读取请求，除非使用了 raw 模式寻址。

可以 \_ \_ 在**nBlockSize**成员中指定 ASYNC 负载*XXX*标志。 Microsoft 建议客户端驱动程序将 **nBlockSize** 成员设置为0，以便 1394 bus driver1394ohci.sys 使用最大支持值，除非使用了 raw 模式寻址。

如果使用 raw 模式寻址，则客户端驱动程序应将 **nBlockSize** 成员设置为设备在连接速度下支持的最大异步负载大小。

有关 raw 模式寻址的详细信息，请参阅在 [IEEE 1394 总线上发送异步 I/o 请求数据包](./sending-asynchronous-i-o-request-packets-on-the-ieee-1394-bus.md)。

[**请求 \_ 异步 \_ 写入**](https://msdn.microsoft.com/library/windows/hardware/ff537636)  

### <a name="uasyncreadnblocksize"></a>AsyncRead. nBlockSize

指定数据流中写入到1394节点的每个块的大小。 如果此参数为零，则使用所选速度的最大数据包大小来划分这些写入请求，除非使用了 raw 模式寻址。

可以 \_ \_ 在**nBlockSize**成员中指定 ASYNC 负载*XXX*标志。 Microsoft 建议客户端驱动程序将 **nBlockSize** 成员设置为0，以便1394总线驱动程序使用最大支持值，除非使用了 raw 模式寻址。

如果使用 raw 模式寻址，则客户端驱动程序应将 **nBlockSize** 成员设置为设备在连接速度下支持的最大异步负载大小。

[**请求 \_ ISOCH \_ 分配 \_ 带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537647)  
可以 \_ \_ 在**fulSpeed**成员中指定速度标志*XXX*标志。 新的1394总线驱动程序可以返回 \_ SpeedSelected 成员中的新速度标志 \_ *XXX*标志。 **SpeedSelected**

### <a name="uisochallocatebandwidthfulspeed"></a>IsochAllocateBandwidth. fulSpeed

指定用于分配带宽的连接速度。 可能的速度值为速度 \_ 标志 \_ *XXX*，其中*xxx*是 (近似) 传输速率（以 mbps 为单位）。

### <a name="uisochallocatebandwidthspeedselected"></a>IsochAllocateBandwidth. SpeedSelected

指定选择分配带宽的实际速度。 该值是一个速度 \_ 标志 \_ *XXX* (请参阅**fulSpeed**成员说明) 。

[**请求 \_ ISOCH \_ 分配 \_ 资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649)  
可以 \_ \_ 在**fulSpeed**成员中指定速度标志*XXX*标志。

### <a name="uisochallocateresourcesfulspeed"></a>IsochAllocateResources. fulSpeed

指定用于在通道上进行通信的连接速度。 可能的速度值为速度 \_ 标志 \_ *XXX*，其中*xxx*是 (近似) 传输速率（以 mbps 为单位）。

[**请求 \_ ISOCH \_ 可用 \_ 带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537652)  
可以 \_ \_ 在**fulSpeed**成员中指定速度标志*XXX*标志。

### <a name="uisochfreebandwidthfulspeed"></a>IsochFreeBandwidth. fulSpeed

指定用于释放带宽的连接速度。 可能的速度值为速度 \_ 标志 \_ *XXX*，其中*xxx*是 (近似) 传输速率（以 mbps 为单位）。

> [!NOTE]
> 仅当设置了 IRB **fulSpeed** \_ 标记 \_ 允许 \_ 远程 \_ 自由标志，并且 IRB \_ 标志 \_ 使用 \_ 预先 \_ 计算 \_ 值标志未在 IRB 的**标志**中设置时，新的 1394 bus 驱动程序才使用 fulSpeed 成员。 在所有其他情况下，新的1394总线驱动程序将忽略 **fulSpeed**。

[**请求 \_ 集 \_ 设备 \_ XMIT \_ 属性**](https://msdn.microsoft.com/library/windows/hardware/ff537662)  
可以 \_ \_ 在**fulSpeed**成员中指定速度标志*XXX*标志。

### <a name="usetdevicexmitpropertiesfulspeed"></a>SetDeviceXmitProperties. fulSpeed

指定到设备的事务的最大速度。 可能的速度值为速度 \_ 标志 \_ *XXX*，其中*xxx*是 (近似) 传输速率（以 mbps 为单位）。

[**请求 \_ 异步 \_ 流**](https://msdn.microsoft.com/library/windows/hardware/ff537635)  
可以 \_ \_ 在**nSpeed**成员中指定速度标志*XXX*标志。

### <a name="uasyncstreamnspeed"></a>AsyncStream. nSpeed

指定传输速率。 可能的速度值为速度 \_ 标志 \_ *XXX*，其中*xxx*是 (近似) 传输速率（以 mbps 为单位）。

[请求 \_ISOCH \_ 修改 \_ 流 \_ 属性](/windows-hardware/drivers/ddi/1394/ns-1394-_irb_req_isoch_modify_stream_properties)可以 \_ \_ 在**fulSpeed**成员中指定速度标志*XXX*标志。

### <a name="uisochmodifystreampropertiesfulspeed"></a>IsochModifyStreamProperties. fulSpeed

指定到设备的事务的最大速度。 可能的速度值为速度 \_ 标志 \_ *XXX*，其中*xxx*是 (近似) 传输速率（以 mbps 为单位）。

[**请求 \_ \_ \_ 在设备之间获取速度 \_**](https://msdn.microsoft.com/library/windows/hardware/ff537645)  
可以 \_ \_ 在**fulSpeed**成员中指定速度标志*XXX*标志。

### <a name="ugetmaxspeedbetweendevicesfulspeed"></a>GetMaxSpeedBetweenDevices. fulSpeed

指定源设备和目标设备集之间可能的最大事务速度。 返回的值是所有设备同时支持的最大速度。 可能的速度值为速度 \_ 标志 \_ *XXX*，其中*xxx*是 (近似) 传输速率（以 mbps 为单位）。

> [!NOTE]
> 客户端驱动程序还可以 \_ \_ 在**GETMAXSPEEDBETWEENDEVICES**中指定 USE SCODE 速度标志，以请求 \_ *XXX* \_ 在**fulSpeed**中返回 SCODE xxx RATE 速度代码值，而不是速度 \_ 标志 \_ XXX 值。

## <a name="related-topics"></a>相关主题

[IEEE 1394 驱动程序堆栈](./the-ieee-1394-driver-stack.md)  
[Windows 7 中的 IEEE 1394 总线驱动程序](./ieee-1394-bus-driver-in-windows-7.md)