---
title: 拓扑微型端口驱动程序
description: 拓扑微型端口驱动程序
ms.assetid: 3e0b797e-2fa5-499b-a465-0f51f5433177
keywords:
- 音频的微型端口驱动程序 WDK 拓扑
- 微型端口驱动程序 WDK 音频拓扑
- 拓扑微型端口驱动程序 WDK 音频
- 拓扑微型端口接口 WDK 音频
- 连接描述符 WDK 音频
- 从节点 WDK 音频
- 在节点 WDK 音频
- 可分辨的节点标识符 WDK 音频
- 混合使用音频 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ac4010e1c670444bb24f68e64809871cdf9068d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354183"
---
# <a name="topology-miniport-driver"></a>拓扑微型端口驱动程序


## <span id="topology_miniport_driver"></span><span id="TOPOLOGY_MINIPORT_DRIVER"></span>


拓扑微型端口驱动程序管理各种硬件中的控件 （例如，卷和静音） 的音频适配器混音器电路。 此驱动程序枚举作为控件*节点*在 mixer 拓扑中，允许客户端发现节点之间的互连和查询并在每个节点设置的控制参数。

[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)生成时查看适配器的拓扑[音频筛选器图形](audio-filter-graphs.md)。 混音器 API （Microsoft Windows SDK 文档的 Windows 多媒体部分中所述） 表示 mixer 行控制，并将其公开到用户模式应用程序，例如 SndVol32 拓扑节点。 有关详细信息，请参阅[任务栏和 SndVol32](systray-and-sndvol32.md)。

拓扑微型端口驱动程序应实现拓扑微型端口接口，该端口驱动程序用于初始化的微型端口驱动程序接口。 微型端口接口[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiporttopology)，继承中的方法[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)接口; 它提供了任何其他方法。 音频适配器驱动程序窗体[拓扑筛选器](topology-filters.md)通过将绑定的微型端口对象 IMiniportTopology 接口到 port 对象的[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology)接口。

通常情况下，拓扑筛选器包含适配器的拓扑节点的大多数尽管适配器内的其他设备可能包含其他拓扑节点。 例如，波形设备，将表示为一个批筛选器，可能包含 DAC ([**KSNODETYPE\_DAC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)) 和 ADC ([**KSNODETYPE\_ADC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-adc)) 节点。

查询和设置的拓扑节点上的控制参数是通过属性请求来实现。 每个节点类型都具有特定属性或组的属性相关联。 节点可能支持只有一个控件值。 例如，卷节点 ([**KSNODETYPE\_卷**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)) 具有一个值，指示其当前的音量设置。 其他节点可能支持多个控件值。 例如，一个三维节点 ([**KSNODETYPE\_3D\_效果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects)) 支持增加的 3D 缓冲区和 3D 侦听程序属性。 Sum 节点 ([**KSNODETYPE\_SUM**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum))，但是，有任何控件值。

拓扑微型端口驱动程序将使用*连接描述符*([**PCCONNECTION\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))) 来描述两个拓扑节点之间的连接。 每个连接为定向，并指定从节点和到节点。 节点可能具有多个插针，并由一个插针执行该函数可能不同于其他球瓶。 为了区分从另一个插针，微型端口驱动程序节点上数字 pin。 在连接描述符出现这些 pin 号码。 例如，状态变量筛选器可能有三个输出插针-分别用于最高价、 中间颜色和低频率的编号为 1、 2 和 3。 插针编号允许微型端口驱动程序的客户端可以确定哪些连接与相关联的 pin。

使用连接描述符*区分节点标识符*， [ **PCFILTER\_节点**](https://docs.microsoft.com/previous-versions/ff537695(v=vs.85))，若要将筛选器上的 pin 与 pin 中的节点上区分开来筛选器。 Mixer 电路的硬编码连接到音频的适配器中音频的呈现和捕获设备的每个表示为固定拓扑筛选器。 其他拓扑筛选器插针表示外部物理连接，例如适配器卡上的线路输出插孔。 拓扑筛选器上的针表示物理、 硬编码连接的适配器硬件。 因此，pin 不能提供显式控制是否建立连接，并且它们不能用于管理通过该连接的数据流。

单个连接描述符可以描述在拓扑中任意两个 pin 类型之间的连接。 上一个连接的两个方面的针都可以是插针上筛选器或筛选器，在节点上的 pin 或连接可以具有一侧上的筛选器 pin 和另一个节点 pin。 微型端口驱动程序指定的连接描述符数组作为其拓扑。 单个 pin 可以有多个连接，这意味着相同的 pin 可以出现在多个数组中的连接描述符。

从微型端口驱动程序获取客户端的拓扑说明未设计为支持如何解释是未知的客户端的节点类型的开放式发现。 节点插针编号单独不提供客户端发现球瓶的函数所需的信息。 尽管微型端口驱动程序 （通过一个 GUID) 标识的节点类型，它不提供任何标准化的参数列表的描述的节点类型或节点类型支持的球瓶。

例如，如果客户端枚举节点使用节点类型 GUID [ **KSNODETYPE\_卷**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)来标识自身，则客户端可以发出它知道的约定时，才使用节点的卷节点处理。 按照约定，卷节点中，例如，支持[ **KSPROPERTY\_音频\_VOLUMELEVEL** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)属性，并将分配节点 pin 编号 0 和 1 到输出 （源） 插针和分别输入 （接收器） 的 pin。 此外，可以控制卷节点通常的客户端执行定向的搜索，用于限制其浏览到相对较少的节点类型 （卷和静音节点，例如）。 客户端通常探讨了仅有可能包含卷节点 （例如，混音器行） 筛选器关系图的部分。

微型端口接口支持未经请求的控件值发生更改的微型端口驱动程序传递到端口驱动程序。 此功能可容纳控件按钮、 滑块或开关可以以物理方式操作由用户的设备。 每次用户更改节点的控件值时，硬件中断通知端口驱动程序的[硬件事件](hardware-events.md)已发生。

 

 




