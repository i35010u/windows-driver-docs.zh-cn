---
title: KS 拓扑注意事项
description: KS 拓扑注意事项
ms.assetid: 81a2a41a-2a10-4de0-9a64-2c8f86a0c96d
keywords:
- 非 PCM 音频格式 WDK，KS 拓扑
- 桥 pin WDK 音频
- mixer API WDK 音频
- KS 筛选器 WDK 音频，非 PCM 波形格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c783e80f14b13c4035474470f0ffa11442d83b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333370"
---
# <a name="ks-topology-considerations"></a>KS 拓扑注意事项


## <span id="ks_topology_considerations"></span><span id="KS_TOPOLOGY_CONSIDERATIONS"></span>


[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)(Wdmaud.sys) 将通过公开的旧 mixer 行转换为 KS 筛选器拓扑**mixer** API。 非 PCM pin 对应于 SRC 行 (MIXERLINE\_COMPONENTTYPE\_SRC\_*XXX*) 混音器 API 中。 如果此 pin 在最终流入桥 pin （物理连接的终结点上的图形） 专用于非 PCM 数据的数据路径**mixer** API 公开为其他的 DST 行 (MIXERLINE桥pin\_COMPONENTTYPE\_DST\_*XXX*)、 独立于 PCM 数据的 DST 行。 这可以通过是否可见的控件添加不必要的复杂性**mixer**如 SndVol32 实用程序的替代-API 客户端。

如果您不想公开非 PCM pin 以这种方式，一种方法是确保最终包含固定的数据路径馈送到由 PCM 数据路径共享的 SUM 节点。 也就是说，将 PCM DST 行联接到主 DST 行。 遗憾的是，此解决方法歪曲 true 硬件拓扑，可能会导致将来问题的客户端来试图控制非 PCM 数据流通过从 SUM 节点下游节点。 更好的方法是修改**mixer**-API 客户端只需忽略 SRC 和 DST 不有任何控件的行。

如果您使用[KsStudio 实用工具](ksstudio-utility.md)若要查看批筛选器在 KSCATEGORY\_音频，您应该会看到不同的 pin 非 PCM 数据。 查看下 KSCATEGORY 复合系统音频图形时\_音频\_设备，你应主要的 wave 输出插针，以及任何 PCM 数据范围上查看非 PCM 数据范围。

SysAudio (Sysaudio.sys) 是在 Windows Server 2003、 Windows XP、 Windows 2000 和 Windows 的系统音频设备我 / 98。 请注意 SysAudio 生成 KSCATEGORY\_音频\_设备自动-驱动程序不应注册自身手动在此类别中。

您不需要连接到拓扑微型端口驱动程序的非 PCM 数据路径。 此连接是拓扑的非常有益仅当非 PCM 数据路径与设备; 的其余部分进行交互例如，如果将馈送到常见 mixer 或采样率转换器。 连接到桥插针，其中这两个 pin 是批微型端口驱动程序，流式处理 pin 窗体为流直接为 S/PDIF 端口，例如某一非 PCM 数据流的有效、 完整拓扑。

 

 




