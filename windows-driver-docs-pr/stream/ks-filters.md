---
title: KS 筛选器
description: KS 筛选器
ms.assetid: caf46279-17f3-4bb4-8b8a-a1673f9fa28f
keywords:
- 筛选 WDK 内核流式处理
- KS 筛选 WDK 内核流式处理
- mixers WDK 内核流式处理
- 内核流 WDK，筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 677ce74374cc7a0e91b84ade977d8b9fadd78533
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842517"
---
# <a name="ks-filters"></a>KS 筛选器





筛选器是一组节点，用于封装要对数据流执行的处理任务。 [Pin](ks-pins.md)充当筛选器上的输入和输出管道。

简单筛选器可以包含一个数据接收器 pin 和一个数据源 pin。 筛选器接收数据接收器 pin 上的传入数据，在内部对其进行处理，并将其写入数据源 pin。 在下图中，这些针脚显示为大直线段。 在内部，筛选器会将数据接收器 pin 连接到内部处理单元（*节点*），而节点又连接到数据源 pin。

![阐释简单 ks 筛选器的关系图](images/ks01.png)

其他设备可能会在 pin 之间合并或拆分数据流。 例如，音频混合器支持多个数据接收器 pin。 混音器将它们合并为一个流，并将该流写入数据源 pin。 下图显示了数据流。

![阐释混音器的示意图](images/ks02.png)

此图描述了筛选器的 pin 之间的内部关系。 更复杂的筛选器可能封装多个节点来转换通过筛选器流动的数据。

筛选器使用[KSPROPSETID\_拓扑](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)属性集来指定引脚和内部节点之间的内部连接。

[**KSPROPERTY\_拓扑\_连接**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-connections)属性查询 KS 筛选器节点之间的所有连接。 此属性返回[**KSTOPOLOGY\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)的数组。 每个 KSTOPOLOGY\_连接结构都表示筛选器内的单个数据路径连接。 在上述混音器关系图中，KSTOPOLOGY\_连接结构的顺序如下所示：

```cpp
//    FromNode,       FromNodePin,     ToNode,        ToNodePin,
{
 {  KSFILTER_NODE,        0,            0,               0     },
 {       0,               1,       KSFILTER_NODE,        1     }
}
```

 

 




