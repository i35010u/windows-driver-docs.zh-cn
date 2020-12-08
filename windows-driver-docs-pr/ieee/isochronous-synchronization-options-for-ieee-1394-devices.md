---
title: IEEE 1394 设备的常时等量同步选项
description: IEEE 1394 设备的常时等量同步选项
keywords:
- 同步 i/o WDK IEEE 1394 总线，同步
- 同步 WDK IEEE 1394 总线
- 筛选 WDK IEEE 1394 总线
- 周期时间同步 WDK IEEE 1394 总线
- 缓冲 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3758677a1964b76fcbdabbdc8c961d8389f8e976
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798215"
---
# <a name="isochronous-synchronization-options-for-ieee-1394-devices"></a>IEEE 1394 设备的常时等量同步选项





在 [**请求 \_ ISOCH \_ 侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655) 和 [**请求 \_ ISOCH \_ 对话**](https://msdn.microsoft.com/library/windows/hardware/ff537660) 操作期间，IEEE 1394 驱动程序堆栈支持某些类型的同步和筛选。

驱动程序可以通过在 \_ \_ \_ \_ \_ \_ 缓冲区的 [**ISOCH \_ 描述符**](/windows-hardware/drivers/ddi/1394/ns-1394-_isoch_descriptor)结构的 **fulFlags** 成员中对标记标记设置 SY 或描述符同步，来启动筛选。 从发送到该缓冲区的数据开始，总线驱动程序将从数据流中删除所有未包含 Sy 或标记值（与 isoch 描述符中指示的 Sy 或标记值相匹配）的数据包。 此筛选将继续执行后面的缓冲区，即使 SY 上的一个描述符 \_ 同步 \_ \_ 和 \_ \_ 标记标志上的描述符同步 \_ 都是在这些缓冲区的 isoch 说明符中设置的。

如果在对 \_ \_ \_ 标记标志的 SY 或描述符同步上设置描述符 \_ 同步 \_ \_ ，则客户端驱动程序还 \_ 会在 \_ 第一个标记中设置描述符 use SY \_ 标记 \_ \_ ，则总线驱动程序将使用 isoch 描述符中的客户端驱动程序提供的 SY 或标记值来同步数据流。 在这种情况下，总线驱动程序会丢弃所有数据包，直到接收到其 Sy 或标记值与 isoch 描述符中指定的值匹配的数据包。 找到匹配项后，总线驱动程序将停止丢弃数据包，并继续将 *所有* 数据包转发到客户端驱动程序。

如果主机控制器支持，则客户端驱动程序可以使用周期时间来同步同步同步数据流。 此上下文中的 "周期时间" 由 [**循环 \_ 时间**](/windows-hardware/drivers/ddi/1394/ns-1394-_cycle_time) 结构定义。 它包括第二个计数、 **cl \_ SecondCount** 每128秒、一个周期计数、 **cl \_ CycleCount**，指示当前秒内已过去的同步循环数，以及一个时钟-滴答计数， **CL \_ CycleOffset**，指示在当前周期内已过去的 IEEE 1394 总线时钟计时周期数。

客户端可以在特定缓冲区中启动同步操作，也可以在某个周期时间同步整个数据流。

若要在特定缓冲区中启动同步操作，客户端驱动程序必须 \_ \_ \_ 在该缓冲区的 Isoch 描述符的 **FULFLAGS** 成员中设置描述符同步时间标志。 它还必须使用将用于同步数据流的周期时间初始化描述符的 **CycleTime** 成员。 在总线驱动程序检查 isoch 描述符后，它将使用指定的周期时间启动同步操作。 总线驱动程序会丢弃所有没有指示的周期时间的数据包，并在找到具有正确周期时间的数据包后恢复传送数据包。

若要在某个周期时间同步整个数据流，客户端驱动程序必须配置一个通道，以便在通道上启动的所有请求都将使用指定的周期时间自动同步数据流。 这提供了一种替代方法，用于根据特定 isoch 描述符的周期时间设置来触发同步。 若要以这种方式配置通道，客户端驱动程序必须执行两个步骤：

1.  当客户端为带有 [**请求 \_ ISOCH \_ 分配 \_ 资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649) 请求的通道分配资源句柄时，它必须 \_ \_ \_ 在 IRB 的 **fulFlags** 成员中设置资源同步时标志。

2.  当客户端请求通道上的侦听或对话操作时，它会指定将用于同步 IRB 的 **StartTime** 成员中的数据流的周期时间。 有关侦听和交谈请求的详细信息，请参阅 [**request \_ ISOCH \_ 侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655) 和 [**请求 \_ ISOCH \_ 对话**](https://msdn.microsoft.com/library/windows/hardware/ff537660)。

若要确定主机控制器是否支持循环时间同步，客户端驱动程序应向总线驱动程序发送 [**请求 " \_ 获取 \_ 本地 \_ 主机 \_ 信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644) " 请求，并将 "IRB" 的 **nLevel** 成员设置为 "2"。 总线驱动程序返回 " [**获取 \_ 本地 \_ 主机" \_ INFO2**](/windows-hardware/drivers/ddi/1394/ns-1394-_get_local_host_info2) 结构以响应此请求。 如果总线驱动程序设置了 \_ \_ "获取本地主机 INFO2" 的 HostCapabilities 成员中的 "主机信息" "支持 \_ 开始 \_ 循环" \_ 标志，则 **HostCapabilities** \_ \_ \_ 表明主机控制器支持使用循环时间同步同步操作。

 

