---
title: 拓扑微型端口驱动程序
description: 拓扑微型端口驱动程序
ms.assetid: 3e0b797e-2fa5-499b-a465-0f51f5433177
keywords:
- 音频微型端口驱动程序 WDK，拓扑
- 微型端口驱动程序 WDK 音频、拓扑
- 拓扑微型端口驱动程序 WDK 音频
- 拓扑微型端口接口 WDK 音频
- 连接描述符 WDK 音频
- from 节点 WDK 音频
- 节点内 WDK 音频
- 可分辨节点标识符 WDK 音频
- 混合音频 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5176f2976e8bbe98b13a840a30f01dce1131311
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832330"
---
# <a name="topology-miniport-driver"></a>拓扑微型端口驱动程序


## <span id="topology_miniport_driver"></span><span id="TOPOLOGY_MINIPORT_DRIVER"></span>


拓扑微型端口驱动程序管理音频适配器混音器线路中的各种硬件控制（例如，音量和静音）。 此驱动程序将控件枚举为混合器拓扑中的*节点*，从而允许客户端发现节点之间的互连，并在每个节点上查询和设置控制参数。

[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)在生成[音频筛选器图](audio-filter-graphs.md)时查看适配器的拓扑。 混音器 API （在 "Microsoft Windows SDK" 文档的 "Windows 多媒体" 部分中介绍）将拓扑节点表示为混音器控件，并将它们公开给用户模式应用程序，如 SndVol32。 有关详细信息，请参阅[SndVol32](systray-and-sndvol32.md)。

拓扑微型端口驱动程序应实现拓扑微型端口接口，端口驱动程序使用该接口来初始化微型端口驱动程序。 微型端口接口[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)继承了[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)接口中的方法;它不提供其他方法。 音频适配器驱动程序通过将微型端口对象的 IMiniportTopology 接口绑定到端口对象的[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)接口形成[拓扑筛选器](topology-filters.md)。

通常，拓扑筛选器包含适配器的大部分拓扑节点，尽管适配器中的其他设备可能包含其他拓扑节点。 例如，波形设备表示为波形滤镜，可能包含 DAC （[**KSNODETYPE\_dac**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)）和 ADC （[**KSNODETYPE\_ADC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-adc)）节点。

拓扑节点上的控制参数的查询和设置是通过属性请求来完成的。 每个节点类型都与一个特定的属性或一组属性相关联。 节点可能仅支持一个控制值。 例如，卷节点（[**KSNODETYPE\_卷**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)）的值指示其当前的音量设置。 其他节点可能支持多个控制值。 例如，3D 节点（[**KSNODETYPE\_3d\_效果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects)）支持多种3d 缓冲区和3d 侦听器属性。 另一方面，sum 节点（[**KSNODETYPE\_sum**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum)）没有控制值。

拓扑微型端口驱动程序使用*连接描述符*（[**PCCONNECTION\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))）来描述两个拓扑节点之间的连接。 将定向每个连接，并同时指定 from 节点和 a 到节点。 一个节点可能有多个 pin，一个 pin 执行的函数可能不同于其他 pin。 为了区分不同的 pin，微型端口驱动程序对节点上的 pin 进行编号。 这些 pin 号显示在连接描述符中。 例如，状态变量筛选器可能有三个输出插针-每个输出插针为高、中和低频率编号1、2和3。 Pin 编号允许微型端口驱动程序的客户端确定哪些连接与哪些 pin 相关联。

连接描述符使用*可分辨节点标识符* [**PCFILTER\_node**](https://docs.microsoft.com/previous-versions/ff537695(v=vs.85))来区分筛选器上的 pin 与筛选器中某个节点上的 pin。 混音器电路的每个硬编码连接到音频设备的音频呈现和捕获设备在拓扑过滤器上都表示为一个固定。 其他拓扑筛选器 pin 表示外部物理连接，例如适配器卡上的 lineout 插孔。 拓扑筛选器上的 pin 表示适配器硬件的物理硬编码连接。 因此，pin 无法显式控制连接是否已建立，并且不能用于管理该连接上的数据流。

单个连接描述符可以描述拓扑中任意两种 pin 类型之间的连接。 连接双方上的插针既可以固定在筛选器上，也可以在筛选器中的节点上固定，也可以在一端使用筛选器并将节点固定在另一端。 微型端口驱动程序将其拓扑指定为连接描述符的数组。 单个 pin 可以有多个连接，这意味着同一个 pin 可以出现在数组中的多个连接描述符中。

客户端从微型端口驱动程序获取的拓扑描述并不用于支持如何对客户端的未知节点类型进行解释的开放式发现。 单独进行节点 pin 编号不会向客户端提供发现 pin 功能所需的信息。 虽然微型端口驱动程序标识节点的类型（通过 GUID），但它不提供任何用于描述节点类型或节点类型支持的 pin 的参数的标准化列表。

例如，如果客户端枚举使用节点类型 GUID [**KSNODETYPE\_卷**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)来标识自身的节点，则仅当客户端知道用于处理卷节点的约定时，才能使用节点。 按照约定，卷节点支持[**KSPROPERTY\_音频\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)属性，并分别将节点 pin 号0和1分配给输出（源）插针和输入（接收器） pin。 此外，能够控制卷节点的客户端通常会执行定向搜索，以限制对相对较少数量节点类型（例如，卷和静音节点）的浏览。 客户端通常仅浏览可能包含卷节点（例如，混音器线）的筛选器图的部分。

微型端口接口支持将未经授权的控制值更改从微型端口驱动程序传递到端口驱动程序。 此功能适用于具有控制旋钮、滑块或交换机的设备，这些设备可由用户进行物理操作。 用户每次更改节点的控制值时，硬件中断都会通知端口驱动程序[硬件事件](hardware-events.md)已发生。

 

 




