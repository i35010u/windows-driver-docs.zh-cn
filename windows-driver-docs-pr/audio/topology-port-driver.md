---
title: 拓扑端口驱动程序
description: 拓扑端口驱动程序
ms.assetid: f671f557-552e-4575-babf-869c8c0b8f08
keywords:
- 拓扑端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频的微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频，端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b39dcdfd03361c868d38b2cb794c10a25d72f8cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328541"
---
# <a name="topology-port-driver"></a>拓扑端口驱动程序


## <span id="topology_port_driver"></span><span id="TOPOLOGY_PORT_DRIVER"></span>


拓扑端口驱动程序公开的音频适配器拓扑的混合使用硬件。 例如，混合了从批呈现器和典型的适配器中的 MIDI 合成器播放流的硬件可以建模为一组控制节点 （卷、 静音和 sum） 和连接节点的数据路径。 此拓扑由 Windows 多媒体 mixer API 公开为一系列控件和 mixer 行 (请参阅[音频 Mixer API 转换到内核流式处理拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md))。 适配器驱动程序提供了相应[拓扑微型端口驱动程序](topology-miniport-driver.md)绑定到拓扑端口驱动程序到窗体[拓扑筛选器](topology-filters.md)。

拓扑端口驱动程序公开[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)微型端口驱动程序的接口。 IPortTopology 方法从接口继承的基[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842); 它提供了任何其他方法。

拓扑端口和微型端口驱动程序对象与彼此通信通过其各自[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)并[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)接口。

 

 




