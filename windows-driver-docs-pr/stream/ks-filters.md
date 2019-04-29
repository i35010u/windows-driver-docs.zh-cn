---
title: KS 筛选器
description: KS 筛选器
ms.assetid: caf46279-17f3-4bb4-8b8a-a1673f9fa28f
keywords:
- 筛选器 WDK 内核流式处理
- KS 筛选器 WDK 内核流式处理
- 搅拌机 WDK 内核流式处理
- 流式处理 WDK，筛选器的内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014f22a144730dcfae711a5508f4b024cd5cb211
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370251"
---
# <a name="ks-filters"></a>KS 筛选器





筛选器是一组封装要在数据流上执行的处理任务的节点。 [Pin](ks-pins.md)充当对筛选器的输入和输出管道。

简单的筛选器可能包含一个数据接收器 pin 和一个数据源的 pin。 筛选器接收的数据接收器插针的传入数据、 在内部，对其进行处理和写入到数据源 pin。 下图中中, 为粗线段显示了球瓶。 筛选器在内部，连接到内部处理单元的数据接收器 pin*节点*，这反过来又连接到数据源 pin。

![说明简单 ks 筛选器的关系图](images/ks01.png)

另一台设备可能会合并或拆分插针之间的数据流。 例如，音频混音器支持多个数据接收器 pin。 Mixer 将它们组合成一个流，并将该流写入数据源 pin。 下图显示了数据流。

![说明一个混音的关系图](images/ks02.png)

在关系图描述筛选器的插针之间的内部关系。 更复杂的筛选器可能会封装转换数据流经筛选器的多个节点。

筛选器使用指定的 pin 和内部节点之间的内部连接[KSPROPSETID\_拓扑](https://msdn.microsoft.com/library/windows/hardware/ff566598)属性集。

[ **KSPROPERTY\_拓扑\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff565802)属性查询 KS 筛选器的节点之间的所有连接。 此属性返回的数组[ **KSTOPOLOGY\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff567148)。 每个 KSTOPOLOGY\_连接结构表示在筛选器内的单个数据路径连接。 在上面的一系列 KSTOPOLOGY 混音器关系图\_连接结构可能按如下所示：

```cpp
//    FromNode,       FromNodePin,     ToNode,        ToNodePin,
{
 {  KSFILTER_NODE,        0,            0,               0     },
 {       0,               1,       KSFILTER_NODE,        1     }
}
```

 

 




