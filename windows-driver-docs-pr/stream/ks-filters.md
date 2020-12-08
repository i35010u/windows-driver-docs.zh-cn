---
title: KS 筛选器
description: KS 筛选器
keywords:
- 筛选 WDK 内核流式处理
- KS 筛选 WDK 内核流式处理
- mixers WDK 内核流式处理
- 内核流 WDK，筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e040b3648a880bd3d7d66e74107fc16c04a604a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792533"
---
# <a name="ks-filters"></a>KS 筛选器





筛选器是一组节点，用于封装要对数据流执行的处理任务。 [Pin](ks-pins.md) 充当筛选器上的输入和输出管道。

简单筛选器可以包含一个数据接收器 pin 和一个数据源 pin。 筛选器接收数据接收器 pin 上的传入数据，在内部对其进行处理，并将其写入数据源 pin。 在下图中，这些针脚显示为大直线段。 在内部，筛选器会将数据接收器 pin 连接到内部处理单元（ *节点*），而节点又连接到数据源 pin。

![阐释简单 ks 筛选器的关系图](images/ks01.png)

其他设备可能会在 pin 之间合并或拆分数据流。 例如，音频混合器支持多个数据接收器 pin。 混音器将它们合并为一个流，并将该流写入数据源 pin。 下图显示了数据流。

![阐释混音器的示意图](images/ks02.png)

此图描述了筛选器的 pin 之间的内部关系。 更复杂的筛选器可能封装多个节点来转换通过筛选器流动的数据。

筛选器使用 [KSPROPSETID \_ 拓扑](./kspropsetid-topology.md) 属性集来指定引脚和内部节点之间的内部连接。

[**KSPROPERTY \_ 拓扑 \_ 连接**](./ksproperty-topology-connections.md)属性查询 KS 筛选器节点之间的所有连接。 此属性返回 [**KSTOPOLOGY \_ 连接**](/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)的数组。 每个 KSTOPOLOGY \_ 连接结构都表示筛选器内的单个数据路径连接。 在上述混音器关系图中，KSTOPOLOGY 连接结构的顺序如下所示 \_ ：

```cpp
//    FromNode,       FromNodePin,     ToNode,        ToNodePin,
{
 {  KSFILTER_NODE,        0,            0,               0     },
 {       0,               1,       KSFILTER_NODE,        1     }
}
```

 

