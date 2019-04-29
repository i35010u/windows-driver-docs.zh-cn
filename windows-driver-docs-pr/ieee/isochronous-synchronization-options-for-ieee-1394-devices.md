---
title: IEEE 1394 设备的常时等量同步选项
description: IEEE 1394 设备的常时等量同步选项
ms.assetid: 27137890-09e7-45d5-b268-7e93c943b489
keywords:
- 同步 I/O WDK IEEE 1394 总线同步
- 同步 WDK IEEE 1394 总线
- 筛选 WDK IEEE 1394 总线
- 周期时间同步 WDK IEEE 1394 总线
- 缓冲区 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5199a6544b01148e52bbc8990077b9023356b91e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371003"
---
# <a name="isochronous-synchronization-options-for-ieee-1394-devices"></a>IEEE 1394 设备的常时等量同步选项





IEEE 1394 驱动程序堆栈支持某些类型的同步和筛选期间[**请求\_ISOCH\_侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655)并[ **请求\_ISOCH\_交谈**](https://msdn.microsoft.com/library/windows/hardware/ff537660)操作。

驱动程序可以启动筛选通过设置描述符\_同步\_ON\_SY 或描述符\_同步\_ON\_中的标记标志**fulFlags**成员缓冲区[ **ISOCH\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537401)结构。 总线驱动程序开始发送到该缓冲区的数据，删除从没有 Sy 数据流或 isoch 描述符中所指示的 Sy 或标记值匹配的标记值的所有数据包。 此筛选过程将继续按照，缓冲区即使描述符的一项也没有\_同步\_ON\_SY 和描述符\_同步\_ON\_isoch 中设置标记标志这些缓冲区的描述符。

如果除了设置描述符\_同步\_ON\_SY 或描述符\_同步\_ON\_标记标志，客户端驱动程序还设置描述符\_使用\_SY\_标记\_IN\_首个标志，总线驱动程序将使用提供的 isoch 描述符同步数据流中的客户端驱动程序的 Sy 或标记值。 在这种情况下，总线驱动程序将放弃所有数据包之前它接收到一个其 Sy 或标记值与 isoch 描述符中所指示的值匹配。 在查找匹配项，总线驱动程序停止放弃数据包，并恢复转发*所有*到客户端驱动程序的数据包。

如果主机控制器支持，客户端驱动程序可以使用周期时间同步的同步数据的流。 在此上下文中的"周期时间"定义由[**周期\_时间**](https://msdn.microsoft.com/library/windows/hardware/ff537067)结构。 它包括第二个计数**CL\_SecondCount**，，包装每隔 128 秒周期计数**CL\_CycleCount**，，该值指示具有的同步周期数在当前的第二个和时钟计时周期计数，已用**CL\_CycleOffset**，指示在当前周期内所经历的 IEEE 1394 总线时钟周期数。

客户端既可以初始化特定缓冲区中的同步操作，或者它可以在一定的周期时间同步整个数据流。

若要启动特定的缓冲区中同步操作，客户端驱动程序必须设置描述符\_同步\_ON\_中的时间标志**fulFlags**的 isoch 描述符的成员缓冲区。 它必须初始化**CycleTime**成员描述符与用于同步的数据流的周期时间。 总线驱动程序将检查 isoch 描述符后，它会启动同步操作使用指定的周期时间。 总线驱动程序将丢弃所有数据包不具有所指示的周期时间，并恢复其在找到具有正确的周期时间数据包传送数据包。

若要在特定的周期时间同步整个数据流，客户端驱动程序必须配置一个通道，以便在通道发起的所有请求会自动都同步数据流使用指示的周期时间。 这提供了一种替代方法触发基于特定 isoch 描述符的周期时间设置的同步。 若要以这种方式配置信道，客户端驱动程序必须执行两个步骤：

1.  当客户端为通道与分配资源句柄[**请求\_ISOCH\_分配\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649)请求，它必须设置资源\_同步\_ON\_中的时间标志**fulFlags** IRB 的成员。

2.  当客户端请求的通道上侦听或讨论操作时，它指定将用于同步在数据流的周期时间**StartTime** IRB 的成员。 详细信息大约侦听和通信的请求，请参阅[**请求\_ISOCH\_侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655)并[**请求\_ISOCH\_对话**](https://msdn.microsoft.com/library/windows/hardware/ff537660)。

若要确定主机控制器支持周期时间同步，是否客户端驱动程序应发送[**请求\_获取\_本地\_主机\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644)总线驱动程序，对请求使用**nLevel** IRB 成员设置为 2。 总线驱动程序将返回[**获取\_本地\_主机\_INFO2** ](https://msdn.microsoft.com/library/windows/hardware/ff537147)以响应此请求的结构。 如果总线驱动程序设置的主机\_INFO\_支持\_启动\_ON\_中的周期标志**HostCapabilities**的 GET 成员\_本地\_主机\_INFO2，这指示主机控制器支持的同步操作使用周期时间同步。

 

 




