---
title: AVStream 拆分器
description: AVStream 拆分器
ms.assetid: c2cfc183-0f4c-4104-a580-234e0483eee4
keywords:
- 拆分条 WDK AVStream
- AVStream 拆分条 WDK
- 将数据拆分流式传输 WDK AVStream
- KSPIN_FLAG_SPLITTER
- 自动拆分 WDK AVStream
- 拆分 WDK AVStream 输入插针
- 处理 WDK AVStream 输出插针拆分器
- 拆分 WDK AVStream pin
- 处理 pin WDK AVStream
- 帧 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2354cda1b30f70a4b52803a515e927d99597e2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386700"
---
# <a name="avstream-splitters"></a>AVStream 拆分器





AVStream 微型驱动程序可以使用 AVStream 类驱动程序的功能将数据流拆分为多个副本，如流通过给定的 pin。 此拆分过程很有用，如果您的驱动程序需要进行复制来生成两个相同的输出流的输入的流。

若要执行此操作，设置 KSPIN\_标志\_中的拆分器**标志**的插针的成员[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。 此标志已设置 pin，pin 充当自动拆分器。 AVStream 会自动将复制拆分流所需的所有数据。

在版本晚于 DirectX8.0，KSPIN\_标志\_拆分器标志 pin 适用于这两者[筛选器以中心](filter-centric-processing.md)和[pin 以中心](pin-centric-processing.md)筛选器。 早期版本支持仅用于插针上筛选器为中心的筛选器的此标志。

下图显示了输入插针将流拆分为两个输出插针的筛选器的配置。 此输出插针的下游筛选器更改数据*就地*。

![说明使用拆分器输出插针 avstream 筛选器的关系图 ](images/split1.png)

帧到达输入插针，并放入输入队列。 微型驱动程序仅与输入的队列和原始 pin 的输出队列进行交互。 AVStream 会自动将数据从第一个 pin 队列复制到第二个插针的队列。

为简单起见，此图不显示如何将帧提供给输出插针。 若要提供输出插针的帧，例如，可能有请求者和与每个队列相关联的分配器和属于本部分中的管道。 或者，帧可能来自下游的筛选器。

在中[ **KSFILTER\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_dispatch)结构，微型驱动程序指定一个指向供应商提供[ *AVStrMiniFilterProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)回调例程。 此回调例程是微型驱动程序，接收一个指向[ **KSPROCESSPIN\_INDEXENTRY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksprocesspin_indexentry)结构，它包含的数组[ **KSPROCESSPIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksprocesspin)结构如下所述。

此图显示了微型驱动程序如何区分两个输出插针，进程 pin 列表中：

![流程图固定表的两个拆分 pin](images/splitppin1.png)

在此图中，DB 指**DelegateBranch**的成员[ **KSPROCESSPIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksprocesspin)结构和 CS 指**CopySource**成员。 这两个**DelegateBranch**并**CopySource**输入插针和第一个输出插针的成员是**NULL**。 这表示微型驱动程序会负责处理这些引脚的帧。

第二个输出插针，但是，具有**CopySource**指回第一个输出插针。 这指示第二个输出插针从第一个输出插针的单独管道中，AVStream 自动复制位于任何数据插入到第二个输出插针的队列中的第一个输出插针的队列。

两个输出插针生成到相同的管道时，可能会出现更复杂的拆分器情况。 微型驱动程序可能包括两个基于拆分器的输出插针中相同的管道，例如，只要下游的筛选器不会更改从这些引脚发送数据。 由于不修改数据，输出插针被视为只读的;这两个下游的筛选器接收相同的缓冲区。

还有可能会自动附加到拆分器 pin 的下游筛选器的一些更改的数据，而其他人则不能。

在这种情况下，筛选器布局可能类似于下图中，描述了包含拆分输出插针的三个实例的筛选器：

![说明具有三个拆分输出插针 avstream 筛选器的关系图 ](images/split2.png)

Pin A 和 B 分配到同一个管道，因为下游的筛选器不会更改数据;筛选器下游的 A 和 B 接收相同的缓冲区指针。

*微型驱动程序仅与输入的队列和单个输出队列进行交互。* AVStream 会自动将复制从 A / B 队列和 C 队列。 它还会创建一个拆分器对象，它将发送的同一个数据帧通过 pin A 和 B 的 pin （请注意，不同的流标头）。

数组[ **KSPROCESSPIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksprocesspin)结构如下所示：

![流程图固定表的三个拆分输出插针](images/splitppin2.png)

仅 pin 与之交互的微型驱动程序必须在正常情况下为 pin a。

若要简化上面的关系图，请求者和分配器中省略关系图。 在关系图用于演示拆分过程框架。

 

 




