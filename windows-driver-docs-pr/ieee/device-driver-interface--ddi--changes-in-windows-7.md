---
title: Windows 7 中的设备驱动程序接口 (DDI) 更改
description: 本主题总结了支持的新的 1394年总线驱动程序的常规 DDI 更改。
ms.assetid: 5473C6AC-284C-41B1-AA67-75696BE96C24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 797a150a27c5f051699e1514944e78ccaf742315
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525310"
---
# <a name="device-driver-interface-ddi-changes-in-windows-7"></a>Windows 7 中的设备驱动程序接口 (DDI) 更改


Windows 7 包括 1394ohci.sys，新的 IEEE 1394 总线驱动程序使用内核模式驱动程序框架 (KMDF) 实现的。 新的 1394年总线驱动程序将替换旧 IEEE 总线中的驱动程序微型端口端口/配置--1394bus.sys 和 ochi1394.sys。 新 DDIs 已添加到 1394ohci.sys 支持的新功能。 此外，某些 1394 DDIs 更改以支持更高速度 1394b 规范定义，并改进了简化的 1394年客户端驱动程序开发。

本主题总结了支持的新的 1394年总线驱动程序的常规 DDI 更改。

-   [扩展的总线重置通知](#extended-bus-reset-notification)
-   [新 Ioctl PHY 数据包支持](#new-ioctls-for-phy-packet-support)
-   [若要检索配置 ROM 的新 IOCTL](#new-ioctl-to-retrieve-configuration-rom)
-   [IEEE 总线驱动程序 DDI 更改](#ieee-bus-driver-ddi-changes)
-   [新标志的速度和有效负载大小](#speed)
-   [IEEE 1394 IOCTL 更改](#ioctl)
-   [相关的主题](#related-topics)

## <a name="extended-bus-reset-notification"></a>扩展的总线重置通知


1394ohci.sys 总线驱动程序支持的扩展的总线重置通知。 此通知总线重置通知的上下文中的 1394年客户端驱动程序返回有关当前生成 （如生成计数和节点 id) 总线的信息。 此信息可以消除对 1394年客户端驱动程序，才能同步检索生成计数、 节点 id 和其他信息，请使用其总线重置通知处理程序的需要。

若要注册扩展的总线重置通知，客户端驱动程序使用的现有[**请求\_总线\_重置\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537638) I/O 请求，并指定新扩展\_通知\_中的例程标志**u.BusResetNotification.fulFlags**参数。 当扩展\_通知\_指定例程标志，则**u.BusResetNotification.ResetContext**参数指向[**总线\_重置\_数据**](https://msdn.microsoft.com/library/windows/hardware/gg266399)结构。

## <a name="new-ioctls-for-phy-packet-support"></a>新 Ioctl PHY 数据包支持


1394ohci.sys 总线驱动程序将公开以下新 DDIs 用于发送和接收 PHY 数据包，因为 IEEE 1394a 规范中定义。

-   [**请求\_发送\_PHY\_数据包**](https://msdn.microsoft.com/library/windows/hardware/gg266407)
-   [**REQUEST\_RECEIVE\_PHY\_PACKETS**](https://msdn.microsoft.com/library/windows/hardware/gg266406)

你应使用新[**请求\_发送\_PHY\_数据包**](https://msdn.microsoft.com/library/windows/hardware/gg266407) I/O 请求，而不是[**请求\_发送\_PHY\_CONFIG\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff537661)。 后一种 I/O 请求不允许用于指定生成计数，这会导致物理数据包发送到的 1394年总线错误生成。

## <a name="new-ioctl-to-retrieve-configuration-rom"></a>若要检索配置 ROM 的新 IOCTL


新 IOCTL， [**请求\_获取\_CONFIG\_ROM**](https://msdn.microsoft.com/library/windows/hardware/gg266404)，返回节点的配置 ROM，最多的最大大小为 1 千字节 (KB) 的内容。 1394ohci.sys 总线驱动程序支持仅为 1 KB 配置 Rom，这是旧的 1394年总线驱动程序相同。

## <a name="ieee-bus-driver-ddi-changes"></a>IEEE 总线驱动程序 DDI 更改


下表描述中的新的 1394年总线驱动程序和旧的 1394年总线驱动程序公开 DDIs 功能行为的更改：

| 设备驱动程序接口                                                              | 描述                                                                                                                                                                                                                                                                          |
|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**请求\_获取\_本地\_主机\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644)             | 1394ohci.sys 总线驱动程序不支持设置**nLevel**与 GET\_主机\_CSR\_内容并指定速度\_映射\_与位置**CsrBaseAddress**。 速度映射是 IEEE 1394a 规范中已过时。                                                                |
| [**请求\_获取\_速度\_拓扑\_映射**](https://msdn.microsoft.com/library/windows/hardware/ff537646)     | [**请求\_获取\_速度\_拓扑\_映射**](https://msdn.microsoft.com/library/windows/hardware/ff537646) Windows 2000 和更高版本的操作系统中已弃用。 将此请求发送到 1394ohci.sys 返回状态\_无效\_参数。                                            |
| [**REQUEST\_GET\_SPEED\_BETWEEN\_DEVICES**](https://msdn.microsoft.com/library/windows/hardware/ff537645) | 发送[**请求\_获取\_速度\_BETWEEN\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff537645) 1394ohci.sys 对请求检索本地节点之间的速度和设备。 使用\_本地\_必须设置节点标志**u.GetMaxSpeedBetweenDevices.fulFlags**参数。 |

 

## <a name="new-flags-for-speed-and-payload-size"></a>新标志的速度和有效负载大小


1394 标头文件，1394.h，Windows 7 Windows 驱动程序工具包中定义新标志更快的速度和更大的有效负载。 本部分介绍这些新标记和值。

下表介绍每种新的受支持的速度的最大异步负载大小。

| Flag                       | 值 | 描述 |
|----------------------------|-------|-------------|
| 异步\_有效负载\_800\_速率  | 4096  | 800 Mb/s    |
| 异步\_有效负载\_1600年\_速率 | 4096  | 160 Mb/s    |
| 异步\_有效负载\_3200\_速率 | 4096  | 3200 Mb/s   |

 

下表介绍每种新的受支持的速度的速度标志。

| Flag               | 值 | 描述 |
|--------------------|-------|-------------|
| 速度\_标志\_800  | 0x08  | 800 Mb/s    |
| SPEED\_FLAGS\_1600 | 0x10  | 160 Mb/s    |
| 速度\_标志\_3200 | 0x20  | 3200 Mb/s   |

 

下表介绍每种新的受支持的速度的速度代码值。

| Flag              | 值 | 描述 |
|-------------------|-------|-------------|
| SCODE\_800\_RATE  | 3     | 800 Mb/s    |
| SCODE\_1600\_RATE | 4     | 160 Mb/s    |
| SCODE\_3200\_RATE | 5     | 3200 Mb/s   |

 

## <a name="ieee-1394-ioctl-changes"></a>IEEE 1394 IOCTL 更改


本部分介绍使用新的速度和有效负载大小值的 1394 I/O 请求。

<a href="" id="request-async-read"></a>[**REQUEST\_ASYNC\_READ**](https://msdn.microsoft.com/library/windows/hardware/ff537634)  
**u.AsyncRead.nBlockSize**

指定在从 1394年节点读取数据流中的每个块的大小。 如果此参数为零，设备和所选的速度的最大数据包大小用于颁发这些读取的请求，除非使用 raw 模式寻址。

您可以指定异步\_有效负载\_*XXX*标记中**nBlockSize**成员。 Microsoft 建议该客户端驱动程序集**nBlockSize**成员为 0，以便 1394年总线 driver1394ohci.sys 使用支持的最大值，除非使用 raw 模式寻址。

如果使用 raw 模式寻址，则应设置客户端驱动程序**nBlockSize**成员添加到支持的设备的连接速度的最大异步负载大小。

Raw 模式寻址的详细信息，请参阅[发送异步 I/O 请求数据包上的 IEEE 1394 总线](https://msdn.microsoft.com/library/windows/hardware/ff538087)。

<a href="" id="request-async-write"></a>[**REQUEST\_ASYNC\_WRITE**](https://msdn.microsoft.com/library/windows/hardware/ff537636)  
**u.AsyncRead.nBlockSize**

指定在写入 1394年节点的数据流中的每个块的大小。 如果此参数为零，则所选的速度的最大数据包大小使用到除这些写入请求时，除非使用 raw 模式寻址。

您可以指定异步\_有效负载\_*XXX*标记中**nBlockSize**成员。 Microsoft 建议该客户端驱动程序集**nBlockSize**成员为 0，以便使用 1394年总线驱动程序支持的最大值，除非使用 raw 模式寻址。

如果使用 raw 模式寻址，则应设置客户端驱动程序**nBlockSize**成员添加到支持的设备的连接速度的最大异步负载大小。

<a href="" id="request-isoch-allocate-bandwidth"></a>[**REQUEST\_ISOCH\_ALLOCATE\_BANDWIDTH**](https://msdn.microsoft.com/library/windows/hardware/ff537647)  
你可以指定速度\_标志\_*XXX*标记中**fulSpeed**成员。 新的 1394年总线驱动程序可以返回新的速度\_标志\_*XXX*标记中**SpeedSelected**成员。

**u.IsochAllocateBandwidth.fulSpeed**

指定要用于分配带宽的连接速度。 可能速度值是速度\_标志\_*XXX*，其中*XXX*是以 mbps 为单位的 （近似） 传输速率。

**u.IsochAllocateBandwidth.SpeedSelected**

指定选择要分配的带宽的实际速度。 值为一个速度\_标志\_*XXX* (请参阅**fulSpeed**成员说明)。

<a href="" id="request-isoch-allocate-resources"></a>[**请求\_ISOCH\_分配\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649)  
你可以指定速度\_标志\_*XXX*标记中**fulSpeed**成员。

**u.IsochAllocateResources.fulSpeed**

指定要用于通信的通道上的连接速度。 可能速度值是速度\_标志\_*XXX*，其中*XXX*是以 mbps 为单位的 （近似） 传输速率。

<a href="" id="request-isoch-free-bandwidth"></a>[**REQUEST\_ISOCH\_FREE\_BANDWIDTH**](https://msdn.microsoft.com/library/windows/hardware/ff537652)  
你可以指定速度\_标志\_*XXX*标记中**fulSpeed**成员。

**u.IsochFreeBandwidth.fulSpeed**

指定要用于可用带宽的连接速度。 可能速度值是速度\_标志\_*XXX*，其中*XXX*是以 mbps 为单位的 （近似） 传输速率。

**请注意**  新的 1394年总线驱动程序将使用**fulSpeed**成员时，才 IRB\_标志\_允许\_远程\_免费标志是组和 IRB\_标志\_使用\_PRE\_CALCULATE\_未设置值标志**标志**IRB。 在所有其他情况下，新的 1394年总线驱动程序将忽略**fulSpeed**。

 

<a href="" id="request-set-device-xmit-properties"></a>[**REQUEST\_SET\_DEVICE\_XMIT\_PROPERTIES**](https://msdn.microsoft.com/library/windows/hardware/ff537662)  
你可以指定速度\_标志\_*XXX*标记中**fulSpeed**成员。

**u.SetDeviceXmitProperties.fulSpeed**

指定设备的最大速度的事务。 可能速度值是速度\_标志\_*XXX*，其中*XXX*是以 mbps 为单位的 （近似） 传输速率。

<a href="" id="request-async-stream"></a>[**REQUEST\_ASYNC\_STREAM**](https://msdn.microsoft.com/library/windows/hardware/ff537635)  
你可以指定速度\_标志\_*XXX*标记中**nSpeed**成员。

**u.AsyncStream.nSpeed**

指定的传输速率。 可能速度值是速度\_标志\_*XXX*，其中*XXX*是以 mbps 为单位的 （近似） 传输速率。

<a href="" id="request-isoch-modify-stream-properties"></a>请求\_ISOCH\_修改\_流\_属性  
你可以指定速度\_标志\_*XXX*标记中**fulSpeed**成员。

**u.IsochModifyStreamProperties.fulSpeed**

指定设备的最大速度的事务。 可能速度值是速度\_标志\_*XXX*，其中*XXX*是以 mbps 为单位的 （近似） 传输速率。

<a href="" id="request-get-speed-between-devices"></a>[**REQUEST\_GET\_SPEED\_BETWEEN\_DEVICES**](https://msdn.microsoft.com/library/windows/hardware/ff537645)  
你可以指定速度\_标志\_*XXX*标记中**fulSpeed**成员。

**u.GetMaxSpeedBetweenDevices.fulSpeed**

指定源设备与目标设备集之间的最大可能的事务速度。 返回的值是所有设备都支持在同一时间的最大速度。 可能速度值是速度\_标志\_*XXX*，其中*XXX*是以 mbps 为单位的 （近似） 传输速率。

**请注意**  客户端驱动程序还可以指定使用\_SCODE\_中的速度标志**u.GetMaxSpeedBetweenDevices.fulFlags**请求的 SCODE\_ *XXX*\_速率速度代码值中返回**fulSpeed**而不是速度\_标志\_xxx 值。

 

## <a name="related-topics"></a>相关主题
[IEEE 1394 驱动程序堆栈](https://msdn.microsoft.com/library/windows/hardware/ff538867)  
[在 Windows 7 中的 IEEE 1394 总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/gg266402)  



