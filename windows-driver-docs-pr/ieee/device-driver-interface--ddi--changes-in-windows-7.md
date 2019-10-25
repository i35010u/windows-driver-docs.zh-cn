---
title: Windows 7 中的设备驱动程序接口 (DDI) 更改
description: 本主题概述了支持新的1394总线驱动程序的常规 DDI 更改。
ms.assetid: 5473C6AC-284C-41B1-AA67-75696BE96C24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2692275893a29f067c68838eaa91017a6e64b904
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841540"
---
# <a name="device-driver-interface-ddi-changes-in-windows-7"></a>Windows 7 中的设备驱动程序接口 (DDI) 更改

Windows 7 包含1394ohci，这是通过使用内核模式驱动程序框架（KMDF）实现的新 IEEE 1394 总线驱动程序。 新的1394总线驱动程序替换端口/微型端口 configuration--1394bus 和 ochi1394 中的旧 IEEE 总线驱动程序。 已将新的 DDIs 添加到1394ohci 支持的新功能中。 此外，某些 1394 DDIs 已更改为支持1394b 规范定义的更多速度，并经过改进，简化了1394客户端驱动程序的开发。

本主题概述了支持新的1394总线驱动程序的常规 DDI 更改。

* [扩展总线重置通知](#extended-bus-reset-notification)
* [用于 PHY 数据包支持的新 IOCTLs](#new-ioctls-for-phy-packet-support)
* [用于检索配置 ROM 的新 IOCTL](#new-ioctl-to-retrieve-configuration-rom)
* [IEEE Bus 驱动程序 DDI 更改](#ieee-bus-driver-ddi-changes)
* [速度和负载大小的新标志](#new-flags-for-speed-and-payload-size)
* [IEEE 1394 IOCTL 更改](#ieee-1394-ioctl-changes)
* [相关主题](#related-topics)

## <a name="extended-bus-reset-notification"></a>扩展总线重置通知

1394ohci 总线驱动程序支持扩展的总线重置通知。 此通知会在总线重置通知上下文中将有关当前的总线（例如生成计数和节点 id）的生成信息返回到1394客户端驱动程序。 利用此信息，无需使用1394客户端驱动程序，就可以使用其总线重置通知处理程序来同步对生成计数、节点 id 和其他信息的检索。

若要注册扩展总线重置通知，客户端驱动程序将使用现有[**请求\_总线\_reset\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537638)i/o 请求，并在 u 中指定新的扩展\_通知\_例程标志 **。BusResetNotification. fulFlags**参数。 指定扩展\_通知\_例程标志后， **BusResetNotification. ResetContext**参数指向[**总线\_重置\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_bus_reset_data)结构。

## <a name="new-ioctls-for-phy-packet-support"></a>用于 PHY 数据包支持的新 IOCTLs

1394ohci 总线驱动程序公开了以下用于发送和接收 PHY 包的新 DDIs，如 IEEE-1394a 规范中所定义。

* [**请求\_发送\_PHY\_数据包**](https://msdn.microsoft.com/library/windows/hardware/gg266407)
* [**请求\_接收\_PHY\_数据包**](https://msdn.microsoft.com/library/windows/hardware/gg266406)

应使用新[**请求\_发送\_phy\_数据包**](https://msdn.microsoft.com/library/windows/hardware/gg266407)i/o 请求，而不是[**请求\_发送\_phy\_配置\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff537661)。 后一 i/o 请求不允许指定生成计数，这可能会导致将 PHY 数据包发送到错误的1394总线生成。

## <a name="new-ioctl-to-retrieve-configuration-rom"></a>用于检索配置 ROM 的新 IOCTL

新的 IOCTL、[**请求\_获取\_CONFIG\_rom**](https://msdn.microsoft.com/library/windows/hardware/gg266404)，返回节点配置 ROM 的内容，最大大小为 1 KB （KB）。 1394ohci 总线驱动程序仅支持 1 KB 配置 Rom，这与旧版1394总线驱动程序相同。

## <a name="ieee-bus-driver-ddi-changes"></a>IEEE Bus 驱动程序 DDI 更改

下表描述了新1394总线驱动程序公开的 DDIs 的功能行为更改和旧1394总线驱动程序：

| 设备驱动程序接口                                                              | 描述                                                                                                                                                                                                                                                                          |
|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**请求\_获取\_本地\_主机\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644)             | 1394ohci 总线驱动程序不支持将**nLevel**设置为\_CSR\_主机\_内容并指定速度\_将\_位置指定为**CsrBaseAddress**。 速度图在 IEEE-1394a 规范中已过时。                                                                |
| [**请求\_获取\_速度\_拓扑\_映射**](https://msdn.microsoft.com/library/windows/hardware/ff537646)     | 在 Windows 2000 和更高版本的操作系统中，[**请求\_获取\_速度\_拓扑\_** ](https://msdn.microsoft.com/library/windows/hardware/ff537646)已弃用。 将此请求发送到1394ohci 返回\_无效\_参数的状态。                                            |
| [**请求\_获取\_设备之间\_速度\_** ](https://msdn.microsoft.com/library/windows/hardware/ff537645) | 发送[**请求\_\_设备请求之间的\_速度\_** ](https://msdn.microsoft.com/library/windows/hardware/ff537645)检索本地节点与设备之间的速度。 必须在**GetMaxSpeedBetweenDevices. fulFlags**参数中设置 USE\_LOCAL\_NODE 标志。 |

## <a name="new-flags-for-speed-and-payload-size"></a>速度和负载大小的新标志

Windows 7 Windows 驱动程序工具包中的1394头文件（即 1394 .h）定义了新标志以提高速度和提高负载。 本部分介绍这些新的标志和值。

下表描述了每个新支持的速度的最大异步负载大小。

| 旗帜                       | Value | 描述 |
|----------------------------|-------|-------------|
| 异步\_负载\_800\_速率  | 4096  | 800 Mb/秒    |
| 异步\_负载\_1600\_速率 | 4096  | 160 Mb/秒    |
| 异步\_负载\_3200\_速率 | 4096  | 3200 Mb/秒   |

下表描述了每个新支持的速度的速度标志。

| 旗帜               | Value | 描述 |
|--------------------|-------|-------------|
| 速度\_标志\_800  | 0x08  | 800 Mb/秒    |
| 速度\_标志\_1600 | 0x10  | 160 Mb/秒    |
| 速度\_标志\_3200 | 0x20  | 3200 Mb/秒   |

下表描述了每个新支持的速度的速度代码值。

| 旗帜              | Value | 描述 |
|-------------------|-------|-------------|
| SCODE\_800\_速率  | 3     | 800 Mb/秒    |
| SCODE\_1600\_速率 | 4     | 160 Mb/秒    |
| SCODE\_3200\_速率 | 5     | 3200 Mb/秒   |

## <a name="ieee-1394-ioctl-changes"></a>IEEE 1394 IOCTL 更改

本部分介绍使用新速度和有效负载大小值的 1394 i/o 请求。

[ **\_异步\_读取请求**](https://msdn.microsoft.com/library/windows/hardware/ff537634)  
**AsyncRead. nBlockSize**

指定数据流中从1394节点读取的每个块的大小。 如果此参数为零，则将使用所选设备的最大数据包大小和所选的速度来发出这些读取请求，除非使用了 raw 模式寻址。

可以在**nBlockSize**成员中指定 ASYNC\_负载\_*XXX*标志。 Microsoft 建议客户端驱动程序将**nBlockSize**成员设置为0，以便 1394 bus driver1394ohci 使用最大支持值，除非使用了 raw 模式寻址。

如果使用 raw 模式寻址，则客户端驱动程序应将**nBlockSize**成员设置为设备在连接速度下支持的最大异步负载大小。

有关 raw 模式寻址的详细信息，请参阅在[IEEE 1394 总线上发送异步 I/o 请求数据包](https://docs.microsoft.com/windows-hardware/drivers/ieee/sending-asynchronous-i-o-request-packets-on-the-ieee-1394-bus)。

[**请求异步\_写入\_** ](https://msdn.microsoft.com/library/windows/hardware/ff537636)  

### <a name="uasyncreadnblocksize"></a>AsyncRead. nBlockSize

指定数据流中写入到1394节点的每个块的大小。 如果此参数为零，则使用所选速度的最大数据包大小来划分这些写入请求，除非使用了 raw 模式寻址。

可以在**nBlockSize**成员中指定 ASYNC\_负载\_*XXX*标志。 Microsoft 建议客户端驱动程序将**nBlockSize**成员设置为0，以便1394总线驱动程序使用最大支持值，除非使用了 raw 模式寻址。

如果使用 raw 模式寻址，则客户端驱动程序应将**nBlockSize**成员设置为设备在连接速度下支持的最大异步负载大小。

[**请求\_ISOCH\_分配\_带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537647)  
可以指定**fulSpeed**成员中\_*XXX*标志的速度\_标志。 新的1394总线驱动程序可以返回**SpeedSelected**成员中\_*XXX*标志的新速度\_标志。

### <a name="uisochallocatebandwidthfulspeed"></a>IsochAllocateBandwidth. fulSpeed

指定用于分配带宽的连接速度。 可能的速度值是\_标志的速度，\_*xxx*，其中*xxx*是（大约）传输速率（以 mbps 为单位）。

### <a name="uisochallocatebandwidthspeedselected"></a>IsochAllocateBandwidth. SpeedSelected

指定选择分配带宽的实际速度。 该值是\_标志的速度之一\_*XXX* （请参阅**fulSpeed**成员说明）。

[**请求\_ISOCH\_分配\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649)  
可以指定**fulSpeed**成员中\_*XXX*标志的速度\_标志。

### <a name="uisochallocateresourcesfulspeed"></a>IsochAllocateResources. fulSpeed

指定用于在通道上进行通信的连接速度。 可能的速度值是\_标志的速度，\_*xxx*，其中*xxx*是（大约）传输速率（以 mbps 为单位）。

[**请求\_ISOCH\_自由\_带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537652)  
可以指定**fulSpeed**成员中\_*XXX*标志的速度\_标志。

### <a name="uisochfreebandwidthfulspeed"></a>IsochFreeBandwidth. fulSpeed

指定用于释放带宽的连接速度。 可能的速度值是\_标志的速度，\_*xxx*，其中*xxx*是（大约）传输速率（以 mbps 为单位）。

> [!NOTE]
> 仅当 IRB\_\_标志设置为 "允许\_远程\_自由标志" 并且 IRB\_标志\_使用\_预先\_计算\_值时，新的 1394 bus 驱动程序才使用**fulSpeed**成员未在 IRB 的**标志**中设置标志。 在所有其他情况下，新的1394总线驱动程序将忽略**fulSpeed**。

[**请求\_集\_设备\_XMIT\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff537662)  
可以指定**fulSpeed**成员中\_*XXX*标志的速度\_标志。

### <a name="usetdevicexmitpropertiesfulspeed"></a>SetDeviceXmitProperties. fulSpeed

指定到设备的事务的最大速度。 可能的速度值是\_标志的速度，\_*xxx*，其中*xxx*是（大约）传输速率（以 mbps 为单位）。

[**请求\_ASYNC\_流**](https://msdn.microsoft.com/library/windows/hardware/ff537635)  
可以指定**nSpeed**成员中\_*XXX*标志的速度\_标志。

### <a name="uasyncstreamnspeed"></a>AsyncStream. nSpeed

指定传输速率。 可能的速度值是\_标志的速度，\_*xxx*，其中*xxx*是（大约）传输速率（以 mbps 为单位）。

[请求\_ISOCH\_修改\_流\_属性](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_irb_req_isoch_modify_stream_properties)可以指定**fulSpeed**成员中\_*XXX*标志的速度\_标志。

### <a name="uisochmodifystreampropertiesfulspeed"></a>IsochModifyStreamProperties. fulSpeed

指定到设备的事务的最大速度。 可能的速度值是\_标志的速度，\_*xxx*，其中*xxx*是（大约）传输速率（以 mbps 为单位）。

[**请求\_获取\_设备之间\_速度\_** ](https://msdn.microsoft.com/library/windows/hardware/ff537645)  
可以指定**fulSpeed**成员中\_*XXX*标志的速度\_标志。

### <a name="ugetmaxspeedbetweendevicesfulspeed"></a>GetMaxSpeedBetweenDevices. fulSpeed

指定源设备和目标设备集之间可能的最大事务速度。 返回的值是所有设备同时支持的最大速度。 可能的速度值是\_标志的速度，\_*xxx*，其中*xxx*是（大约）传输速率（以 mbps 为单位）。

> [!NOTE]
> 客户端驱动程序还可以在**fulFlags**中指定 USE\_SCODE\_速度标志，以请求在**fulSpeed**而不是速度中返回 SCODE\_*XXX*\_速率代码值\_xxx 值\_标志。

## <a name="related-topics"></a>相关主题

[IEEE 1394 驱动程序堆栈](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)  
[Windows 7 中的 IEEE 1394 总线驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)  
