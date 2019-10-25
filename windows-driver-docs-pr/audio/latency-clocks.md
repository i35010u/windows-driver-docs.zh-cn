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
ms.openlocfilehash: d785389606d4b2a2c4b21c89c5ed928f657cb3a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832662"
---
# <a name="latency-clocks"></a>延迟时钟


## <span id="latency_clocks"></span><span id="LATENCY_CLOCKS"></span>


合成器微型端口驱动程序型号旨在允许在多个设备之间同步音频输出。 在这种情况下，它包含的计时模型比纯 UART 设备提供的更复杂。

使用关联的时间戳将事件传送到（以及从中捕获）小型端口驱动程序。 此时间戳相对于[主时钟](https://docs.microsoft.com/windows-hardware/drivers/stream/master-clocks)。 主时钟是整个系统中的所有序列使用的时钟。 主时钟时间以100毫微秒刻度为单位。

微型端口驱动程序通过调用[**IMasterClock：： GetTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imasterclock-gettime)获取主时钟的当前时间。 在创建 pin 时，端口驱动程序将内核模式[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)接口传递到微型端口驱动程序，作为[**IMiniportDMus：： newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)方法的输入参数之一。 目前，主时钟会包装系统实时时钟。 如果有要求其处于*运行*状态的 pin，则主时钟从不会更改。 它是从不暂停的恒定速率时钟。

所有呈现设备在接受事件的时间与事件可以听到的时间之间存在一定程度的延迟。 此延迟可以是常量或可变的（如软件合成器的情况，延迟取决于音频缓冲区的当前播放位置）。 此延迟的补偿方式如下：

-   允许 Dmu 微型端口驱动程序提前接收事件，以便能够按时播放事件，尽管设备滞后时间。 Dmu 端口驱动程序中的序列化引擎对小型端口驱动程序的事件进行排序。

    在创建 pin 时，端口驱动程序会以100毫微秒为单位查询微型端口驱动程序的增量时间。 此增量时间是每个事件的显示时间比小型端口驱动程序要接收事件的时间。 端口驱动程序会尽力实现此功能。 为此增量指定非常大的值（由[**IMiniportDMus：： newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)的*SchedulePreFetch*参数指定），会使端口驱动程序在从用户模式传递到端口驱动程序后立即将事件传递给微型端口驱动程序。

-   向应用程序通知计划事件的进度。 在这种情况下，不需要使用最大延迟。 由于事件在提交后就无法取消，因此，可以将事件提交到其表示时间，从而使应用程序和合成可以交互的对象越多。 为了满足此要求，DirectMusic 已引入了延迟时钟的概念。

    延迟时钟提供将来可计划事件播放并在时间上播放的最近时间。 换言之，如果应用程序计划在当前时间之前根据延迟时钟播放事件，则该事件会延迟播放。 合成器微型端口驱动程序通过响应[**KSPROPERTY\_合成\_LATENCYCLOCK**](https://docs.microsoft.com/previous-versions/ff537402(v=vs.85))属性项来提供延迟时钟。

    \_合成\_LATENCYCLOCK 的[KSPROPSETID\_合成](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth)和 KSPROPERTY 查询微型端口驱动程序。 微型端口驱动程序的属性处理程序应返回延迟时钟，该时钟指定了在下一次可以按时间呈现数据时的主时钟。 例如，如果主时钟当前读取了50，当前有25个单位的延迟，则延迟时间将为75。 以这种方式实现时钟的原因是，延迟无需是常量，返回值比只是增量更用于应用程序。

 

 




