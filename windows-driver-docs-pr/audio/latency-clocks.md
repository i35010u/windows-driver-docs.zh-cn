---
title: 延迟时钟
description: 延迟时钟
ms.assetid: 3cdd4c69-d99d-48bc-a1d9-9da2a2511e94
keywords:
- 合成器 WDK 音频，延迟时钟
- 延迟 WDK 音频、 时钟
- 时钟 WDK 音频延迟
- 滞后时间的 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e14b663a16475553e3eaa8a8c10e2b7ccad643de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332431"
---
# <a name="latency-clocks"></a>延迟时钟


## <span id="latency_clocks"></span><span id="LATENCY_CLOCKS"></span>


合成器微型端口驱动程序模型旨在允许同步多个设备之间的音频输出。 在这种情况下，它包含所提供的纯 UART 设备相比更复杂的计时模型。

传递到 （和从捕获） 事件关联的时间戳的微型端口驱动程序。 此时间戳是相对于[主时钟](https://msdn.microsoft.com/library/windows/hardware/ff567717)。 主时钟是整个系统中的所有序列化使用的同一个时钟。 Master 时钟时间被以 100 毫微秒为单位的单位。

微型端口驱动程序通过调用从主时钟获取当前时间[ **IMasterClock::GetTime**](https://msdn.microsoft.com/library/windows/hardware/ff536697)。 在 pin 创建时，端口驱动程序通过了内核模式[IMasterClock](https://msdn.microsoft.com/library/windows/hardware/ff536696)微型端口驱动程序，因为其中一个输入参数的接口[ **IMiniportDMus::NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536701)方法。 目前，主时钟包装系统实时时钟。 它是在需要的 pin 时永远不会更改主时钟*运行*状态。 它是永远不会暂停常量速率时钟。

呈现的所有设备进行都一定量的接受事件的时间和可以听到该事件的时间之间的延迟。 此延迟可能是常量或变量 （如中所示的软件合成器，其中延迟取决于当前播放位置音频缓冲区的大小写）。 这种延迟被弥补：

-   允许 Dmu 微型端口驱动程序足够的距离提前接收事件，以便它们可以播放时，尽管该设备的延迟。 微型端口驱动程序的事件是由排序器引擎 Dmu 端口驱动程序中序列化。

    在 pin 创建时，端口驱动程序以 100 毫微秒为单位的增量时间查询微型端口驱动程序。 此时间变化量是多久之前微型端口驱动程序想要接收事件的每个事件的呈现时间。 端口驱动程序使其最大程度地将事件传送这得预。 指定此增量非常大的值 (由指定*SchedulePreFetch*的参数[ **IMiniportDMus::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536701)) 使端口驱动程序传递到事件微型端口驱动程序就立即传送到端口驱动程序从用户模式。

-   通知应用程序如何提前计划事件。 使用的最大延迟不应在这种情况下。 因为不能取消事件，一旦提交，越接近，事件可以将应用提交到其呈现时间，响应能力更强的应用程序和合成器可以进行交互。 若要处理这一要求，DirectMusic 引入了延迟时钟的概念。

    延迟时钟提供的最近时间在将来可计划事件的播放和仍在时间上播放。 换而言之，如果应用程序计划根据延迟时钟的当前时间之前要播放的事件，将晚期播放事件。 合成器微型端口驱动程序通过响应提供延迟时钟[ **KSPROPERTY\_合成\_LATENCYCLOCK** ](https://msdn.microsoft.com/library/windows/hardware/ff537402)属性项。

    微型端口驱动程序中查询[KSPROPSETID\_合成](https://msdn.microsoft.com/library/windows/hardware/ff537486)和 KSPROPERTY\_合成器\_LATENCYCLOCK。 微型端口驱动程序的属性处理程序应返回根据主时钟，指定可以在时间呈现数据的下一步时间延迟时钟。 例如，如果主时钟目前为 50，并且当前有 25 个单位的延迟，延迟时钟将为 75。 在这种方式中实现时钟的原因是，延迟不需要是恒定的并且返回的值是只是增量比使用更多应用程序。

 

 




