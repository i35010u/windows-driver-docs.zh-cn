---
title: 拓扑端口驱动程序
description: 拓扑端口驱动程序
ms.assetid: f671f557-552e-4575-babf-869c8c0b8f08
keywords:
- 拓扑端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频、端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78afd447dd12d56bacaa5e564791245a373c8fd2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829990"
---
# <a name="topology-port-driver"></a>拓扑端口驱动程序


## <span id="topology_port_driver"></span><span id="TOPOLOGY_PORT_DRIVER"></span>


拓扑端口驱动程序显示音频适配器混合硬件的拓扑。 例如，将播放流混合到典型适配器中的波形呈现器和 MIDI 合成器的硬件可以建模为一组控制节点（卷、静音和总和）以及连接节点的数据路径。 Windows 多媒体混音器 API 将此拓扑公开为一组控件和混音器（请参阅[音频混音器 Api 转换的内核流拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md)）。 适配器驱动程序提供了相应的[拓扑微型端口驱动程序，该驱动程序](topology-miniport-driver.md)绑定到拓扑结构的驱动程序以形成[拓扑筛选器](topology-filters.md)。

拓扑端口驱动程序向微型端口驱动程序公开[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)接口。 IPortTopology 继承基接口[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)中的方法;它不提供其他方法。

拓扑端口和微型端口驱动程序对象通过各自的[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)和[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)接口相互通信。

 

 




