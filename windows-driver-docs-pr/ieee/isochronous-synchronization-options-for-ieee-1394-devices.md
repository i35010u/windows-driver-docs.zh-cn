---
title: IEEE 1394 设备的常时等量同步选项
description: IEEE 1394 设备的常时等量同步选项
ms.assetid: 27137890-09e7-45d5-b268-7e93c943b489
keywords:
- 同步 i/o WDK IEEE 1394 总线，同步
- 同步 WDK IEEE 1394 总线
- 筛选 WDK IEEE 1394 总线
- 周期时间同步 WDK IEEE 1394 总线
- 缓冲 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d16aaa9f3ddf6be51eb48357b133a9ccc8733a84
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841535"
---
# <a name="isochronous-synchronization-options-for-ieee-1394-devices"></a>IEEE 1394 设备的常时等量同步选项





在请求期间，IEEE 1394 驱动程序堆栈支持特定类型的同步和筛选[ **\_ISOCH\_侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655)和[**请求\_ISOCH\_交谈**](https://msdn.microsoft.com/library/windows/hardware/ff537660)操作。

驱动程序可以通过设置缓冲区的[**ISOCH\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_isoch_descriptor)结构的**fulFlags**成员中\_标记标志上的描述符\_同步\_\_\_来启动筛选。 从发送到该缓冲区的数据开始，总线驱动程序将从数据流中删除所有未包含 Sy 或标记值（与 isoch 描述符中指示的 Sy 或标记值相匹配）的数据包。 此筛选继续执行后面的缓冲区，即使在\_SY 上的一个描述符\_同步\_并在这些缓冲区的 isoch 说明符中设置\_标记标志上的描述符\_同步\_也是如此。

如果在\_SY 或描述符上设置描述符\_同步\_\_同步\_上的\_标记标志，则客户端驱动程序还会将描述符\_使用\_SY\_标记\_在\_第一个标志中，总线驱动程序将使用 isoch 描述符中的客户端驱动程序提供的 Sy 或标记值来同步数据流。 在这种情况下，总线驱动程序会丢弃所有数据包，直到接收到其 Sy 或标记值与 isoch 描述符中指定的值匹配的数据包。 找到匹配项后，总线驱动程序将停止丢弃数据包，并继续将*所有*数据包转发到客户端驱动程序。

如果主机控制器支持，则客户端驱动程序可以使用周期时间来同步同步同步数据流。 此上下文中的 "周期时间" 由[**循环\_时间**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_cycle_time)结构定义。 它包含第二个计数， **CL\_SecondCount**，每128秒包装一次，一个周期计数， **CL\_CycleCount**，指示当前秒内已用时的同步周期数和一个时钟滴答计数。**CL\_CycleOffset**，它指示在当前周期内已过去的 IEEE 1394 总线时钟计时周期数。

客户端可以在特定缓冲区中启动同步操作，也可以在某个周期时间同步整个数据流。

若要在特定缓冲区中启动同步操作，客户端驱动程序必须在该缓冲区的 isoch 描述符的**fulFlags**成员中设置描述符\_同步\_\_。 它还必须使用将用于同步数据流的周期时间初始化描述符的**CycleTime**成员。 在总线驱动程序检查 isoch 描述符后，它将使用指定的周期时间启动同步操作。 总线驱动程序会丢弃所有没有指示的周期时间的数据包，并在找到具有正确周期时间的数据包后恢复传送数据包。

若要在某个周期时间同步整个数据流，客户端驱动程序必须配置一个通道，以便在通道上启动的所有请求都将使用指定的周期时间自动同步数据流。 这提供了一种替代方法，用于根据特定 isoch 描述符的周期时间设置来触发同步。 若要以这种方式配置通道，客户端驱动程序必须执行两个步骤：

1.  当客户端为带有[**请求\_ISOCH\_分配\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649)请求的通道分配资源句柄时，它\_\_必须在 " **fulFlags** " 成员的IRB.

2.  当客户端请求通道上的侦听或对话操作时，它会指定将用于同步 IRB 的**StartTime**成员中的数据流的周期时间。 有关侦听和交谈请求的详细信息，请参阅[**request\_ISOCH\_侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655)和[**请求\_ISOCH\_交谈**](https://msdn.microsoft.com/library/windows/hardware/ff537660)。

若要确定主机控制器是否支持循环时间同步，客户端驱动程序应发送请求，\_获取到总线驱动程序[ **\_本地\_主机\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644)请求，并将 IRB 的**nLevel**成员设置为2。 总线驱动程序将返回[ **\_本地\_主机\_INFO2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_get_local_host_info2)结构，以响应此请求。 如果总线驱动程序将主机\_信息\_在 GET\_本地\_主机\_INFO2 的**HostCapabilities**成员中的\_循环标志\_支持 START\_，这表示宿主控制器支持使用循环时间同步同步操作。

 

 




