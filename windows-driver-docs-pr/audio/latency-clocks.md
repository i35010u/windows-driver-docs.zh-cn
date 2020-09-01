---
title: 延迟时钟
description: 延迟时钟
ms.assetid: 3cdd4c69-d99d-48bc-a1d9-9da2a2511e94
keywords:
- 合成 WDK 音频，延迟时钟
- 延迟 WDK 音频，时钟
- 时钟 WDK 音频，延迟
- 延迟 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e37638061d42eca3ab60389bc6a80bf5ed2f6ee
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208825"
---
# <a name="latency-clocks"></a>延迟时钟


## <span id="latency_clocks"></span><span id="LATENCY_CLOCKS"></span>


合成器微型端口驱动程序型号旨在允许在多个设备之间同步音频输出。 在这种情况下，它包含的计时模型比纯 UART 设备提供的更复杂。

事件会传递到 (，并) 使用关联时间戳的小型小型驱动程序进行捕获。 此时间戳相对于 [主时钟](../stream/master-clocks.md)。 主时钟是整个系统中的所有序列使用的时钟。 主时钟时间以100毫微秒刻度为单位。

微型端口驱动程序通过调用 [**IMasterClock：： GetTime**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imasterclock-gettime)获取主时钟的当前时间。 在创建 pin 时，端口驱动程序将内核模式 [IMasterClock](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock) 接口传递到微型端口驱动程序，作为 [**IMiniportDMus：： newstream.ischecked**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream) 方法的输入参数之一。 目前，主时钟会包装系统实时时钟。 如果有要求其处于 *运行* 状态的 pin，则主时钟从不会更改。 它是从不暂停的恒定速率时钟。

所有呈现设备在接受事件的时间与事件可以听到的时间之间存在一定程度的延迟。 这种延迟可以是常量，也可以是可变 (如软件合成器，延迟取决于音频缓冲区的当前播放位置) 。 此延迟的补偿方式如下：

-   允许 Dmu 微型端口驱动程序提前接收事件，以便能够按时播放事件，尽管设备滞后时间。 Dmu 端口驱动程序中的序列化引擎对小型端口驱动程序的事件进行排序。

    在创建 pin 时，端口驱动程序会以100毫微秒为单位查询微型端口驱动程序的增量时间。 此增量时间是每个事件的显示时间比小型端口驱动程序要接收事件的时间。 端口驱动程序会尽力实现此功能。 为此增量 (指定一个非常大的值[**IMiniportDMus：：) newstream.ischecked**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)的*SchedulePreFetch*参数指定的值将使端口驱动程序在从用户模式传递到端口驱动程序后立即将这些事件传递给微型端口驱动程序。

-   向应用程序通知计划事件的进度。 在这种情况下，不需要使用最大延迟。 由于事件在提交后就无法取消，因此，可以将事件提交到其表示时间，从而使应用程序和合成可以交互的对象越多。 为了满足此要求，DirectMusic 已引入了延迟时钟的概念。

    延迟时钟提供将来可计划事件播放并在时间上播放的最近时间。 换言之，如果应用程序计划在当前时间之前根据延迟时钟播放事件，则该事件会延迟播放。 合成器微型端口驱动程序通过响应 [**KSPROPERTY \_ 合成 \_ LATENCYCLOCK**](/previous-versions/ff537402(v=vs.85)) 属性项提供延迟时钟。

    为 [KSPROPSETID \_ 合成](./kspropsetid-synth.md) LATENCYCLOCK 和 KSPROPERTY 合成查询微型端口驱动程序 \_ \_ 。 微型端口驱动程序的属性处理程序应返回延迟时钟，该时钟指定了在下一次可以按时间呈现数据时的主时钟。 例如，如果主时钟当前读取了50，当前有25个单位的延迟，则延迟时间将为75。 以这种方式实现时钟的原因是，延迟无需是常量，返回值比只是增量更用于应用程序。

 

