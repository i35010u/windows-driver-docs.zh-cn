---
title: AVStream 拆分器
description: AVStream 拆分器
ms.assetid: c2cfc183-0f4c-4104-a580-234e0483eee4
keywords:
- 拆分 WDK AVStream
- AVStream 拆分器 WDK
- 拆分数据流 WDK AVStream
- KSPIN_FLAG_SPLITTER
- 自动拆分 WDK AVStream
- 输入插针拆分 WDK AVStream
- 输出插针拆分器处理 WDK AVStream
- 固定的 AVStream WDK
- 处理 pin WDK AVStream
- 帧 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4bab8ff64453ff32a6b72abb075496008264889
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840622"
---
# <a name="avstream-splitters"></a>AVStream 拆分器





当流通过给定的 pin 传递时，AVStream 微型驱动程序可以使用 AVStream 类驱动程序功能将数据流拆分为多个副本。 如果你的驱动程序需要复制输入流以生成两个相同的输出流，则此拆分过程会很有用。

若要执行此操作，请将 KSPIN\_标记设置\_拆分**器标记在**Pin 的[**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构。 如果在 pin 上设置此标志，则 pin 将充当自动拆分器。 AVStream 会自动复制拆分流所需的所有数据。

在低于 DirectX 8.0 的版本中，KSPIN\_标志\_拆分器标志适用于以[筛选器为](filter-centric-processing.md)中心和以[针为中心](pin-centric-processing.md)的筛选器上的 pin。 以前的版本仅支持在以筛选器为中心的筛选器上的 pin。

下图显示了一个筛选器的配置，其中输入插针将流拆分为两个输出插针。 此输出 pin 的下游筛选器会更改数据*就地*。

![阐释带有拆分器输出插针的 avstream 筛选器的关系图 ](images/split1.png)

帧到达输入插针，并放入输入队列。 微型驱动程序仅与输入队列和原始 pin 的输出队列交互。 AVStream 自动将数据从第一个插针的队列复制到第二个 pin 的队列。

为简单起见，此图不显示如何将帧提供给输出插针。 例如，若要为输出插针提供帧，则可能有一个请求方和分配器与每个队列相关联，并且属于此管道部分。 或者，框架可能来自下游筛选器。

在[**KSFILTER\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)结构中，微型驱动程序指定一个指向供应商提供的[*AVStrMiniFilterProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)回调例程的指针。 此回调例程用于接收指向[**KSPROCESSPIN\_INDEXENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin_indexentry)结构的指针，该指针包含下面描述的[**KSPROCESSPIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin)结构的数组。

此图显示了微型驱动程序如何区分 "进程插针" 列表中的两个输出插针：

![两个拆分针脚的进程引脚表示意图](images/splitppin1.png)

在此关系图中，DB 引用[**KSPROCESSPIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin)结构的**DelegateBranch**成员，而 CS 引用**CopySource**成员。 输入插针和第一个输出插针的**DelegateBranch**和**CopySource**成员均为**NULL**。 这表示微型驱动程序负责处理这些引脚上的帧。

但是，第二个输出插针有一个**CopySource** ，它指向第一个输出插针。 这表示第二个输出插针位于第一个输出插针的单独管道中，AVStream 会自动将放置在第一个输出插针的队列中的任何数据复制到第二个输出插针的队列中。

当两个输出插针内置于同一管道时，可能会出现更复杂的拆分器情况。 例如，微型驱动程序可以在同一管道中包含两个基于拆分器的输出插针，前提是下游筛选器不更改从这些 pin 发送的数据。 由于未修改数据，因此输出插针被视为只读。这两个下游筛选器都接收相同的缓冲区。

还可能会自动附加到拆分器 pin 的某些下游筛选器会更改数据，而另一些则不会。

在这种情况下，筛选器布局可能类似于下图，该图描述了包含拆分输出插针三个实例的筛选器：

![说明具有三个拆分输出插针的 avstream 筛选器的关系图 ](images/split2.png)

由于下游筛选器不更改数据，因此会将引脚 A 和 B 分配给同一管道;和 B 的下游筛选器接收相同的缓冲区指针。

*微型驱动程序仅与输入队列和单个输出队列交互。* AVStream 自动从 A/B 队列和 C 队列复制。 它还会创建一个拆分器对象，该对象通过 pin A 和 pin B 发送相同的数据帧（请注意，流标头会有所不同）。

[**KSPROCESSPIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin)结构的数组如下所示：

![三个拆分输出插针的进程引脚表示意图](images/splitppin2.png)

在正常情况下，微型驱动程序必须与之交互的唯一 pin 是固定的。

为了简化以上关系图，关系图中省略了请求者和分配器。 关系图仅用于演示帧拆分进程。

 

 




