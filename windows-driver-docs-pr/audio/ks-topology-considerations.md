---
title: KS 拓扑注意事项
description: KS 拓扑注意事项
keywords:
- 非 PCM 音频格式 WDK，KS 拓扑
- 桥接 WDK 音频
- 混音器 API WDK 音频
- KS 筛选 WDK 音频，非 PCM 波浪格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de92beb5f8ab54908aa3b807fd20c659e6e26e1a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799217"
---
# <a name="ks-topology-considerations"></a>KS 拓扑注意事项


## <span id="ks_topology_considerations"></span><span id="KS_TOPOLOGY_CONSIDERATIONS"></span>


[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver) ( # A0) 会将 KS 筛选器拓扑转换为通过 **混音** 器 API 公开的旧版混音器。 在混音器 API 中，非 PCM pin 对应于 SRC 行 (MIXERLINE \_ COMPONENTTYPE \_ SRC \_ *XXX*) 。 如果此 pin 位于某个数据路径中，而该路径最终流入了一个桥 (接的数据路径中，而该物理连接位于) 专用于非 PCM 数据的图形的端点，则 **混音** 器 API 会将桥接 \_ \_ \_ *XXX*) MIXERLINE 作为附加的 DST 线路， ( 这可能会给通过 **混音** 器 API 客户端可见的控件增加不必要的复杂性，例如替换 SndVol32 实用程序。

如果你不想以这种方式公开非 PCM pin，一种方法是确保包含该 pin 的数据路径最终源到由 PCM 数据路径共享的 SUM 节点。 也就是说，将非 PCM DST 行加入主 DST 行。 遗憾的是，这种解决方法歪曲了真实的硬件拓扑，并可能导致客户端在尝试通过 SUM 节点下游的节点控制非 PCM 数据流时出现问题。 更好的方法是修改 **混音** 器 API 客户端，以便只忽略没有控件的 SRC 和 DST 行。

如果使用 [KsStudio 实用工具](ksstudio-utility.md) 在 KSCATEGORY 音频中查看波形筛选器 \_ ，应会看到非 PCM 数据的单独 pin。 查看 "KSCATEGORY 音频设备" 下的 "复合系统音频" 图形时 \_ \_ ，应会看到主波形输出插针上的非 pcm 数据范围以及任何 PCM 数据范围。

SysAudio ( # A0) 是 Windows Server 2003、Windows XP、Windows 2000 和 Windows Me/98 中的系统音频设备。 请注意，SysAudio \_ 会自动生成 KSCATEGORY 音频 \_ 设备，驱动程序不应在此类别中手动注册自身。

不需要将非 PCM 数据路径连接到拓扑微型端口驱动程序。 仅当非 PCM 数据路径与设备拓扑的其余部分进行交互时，此连接才有用;例如，如果它送入公共混音器或采样率转换器。 将流 pin 连接到桥接，其中两个插针都位于波形微型端口驱动程序上，为直接流向 S/PDIF 端口的非 PCM 数据流形成有效的完整拓扑。

 

 




