---
title: 输入装配器阶段
description: 输入装配器阶段
ms.assetid: 8db6a2ab-8354-4690-8141-2cdd91c77d5c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa2a2f0d0065c4562b7aab79374e648305a49a66
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350253"
---
# <a name="input-assembler-stage"></a>输入装配器阶段


输入装配器 (IA) 带来三角形、 线或点到呈现管道通过将源超出 1d 缓冲区的几何图形数据提取。

顶点数据可以来自多个缓冲区，可从每个缓冲区的数组的结构方式访问。 缓冲区是每个绑定到单个输入槽，给定结构跨距。 在其中定义了每个条目的输入声明指定所有缓冲区上的数据布局*元素*。 该元素包含输入的槽、 结构偏移量、 数据类型和目标寄存器 （适用于管道中的第一个活动着色器）。

从缓冲区中提取的数据构建给定的序列的顶点。 定向的遍历中的固定函数状态并可使用多种组合来提取的数据*绘制\** DDI （） 调用。 各种基元的拓扑 （例如，点列表、 行列表、 三角形列表和三角形条带） 是可用于使表示一个序列的基元的顶点数据序列。

可以通过两种方式之一生成顶点数据。 若要生成的顶点数据的第一个方法是*非索引*呈现，这是包含顶点数据的缓冲区的顺序遍历。 顶点数据之后，在每个缓冲区绑定的起始偏移量位置处。 若要生成的顶点数据的第二个方法是*编制索引*呈现，这是一个缓冲区包含标量整数索引的顺序遍历。 索引源自到缓冲区的起始偏移量。 每个索引指示位置提取出包含顶点数据的缓冲区的数据。 索引值均独立于其引用的缓冲区的特征。 通过声明描述缓冲区。 未编制索引和索引呈现，在其自己的方式，每个生成从中提取顶点数据在内存中，地址，并随后将结果组装到顶点和基元。

通过允许在非索引或索引呈现时，若要循环访问每个顶点缓冲区 （未编制索引的情况下） 中的范围或索引缓冲区 （索引大小写） 的顺序遍历，启用实例化的 geometry 呈现。 缓冲区绑定将被视为*实例数据*或*顶点数据*。 此标识指定如何执行实例化的呈现时使用的绑定的缓冲区。 地址生成的非索引或索引的呈现用于提取顶点数据，也可以计算为循环时，运行时执行实例化的呈现。 实例数据，但是，始终按顺序开始遍历从每个缓冲区的偏移量，在每个实例 （例如，正向后遍历的顶点数实例中的一个步骤） 的一个步骤的频率。 此外可以选择步骤速率为实例数据为实例频率 （即，一个步骤前滚其他所有实例，每个第三个实例，依次类推） 子调和。

IA 的另一种特殊情况是，它可以读取流输出阶段的缓冲区写入。 此类方案，可以使新类型的绘制操作[ **DrawAuto**](https://msdn.microsoft.com/library/windows/hardware/ff556123)。 *DrawAuto*允许动态少量的输出写入到流输出缓冲区可以重复使用、 无需 CPU 干预，以确定实际写入的数据量。

除了生成顶点缓冲区中的数据，IA 可以自动生成三个标量计数器值：VertexID、 PrimitiveID 和实例 Id，用于呈现管道中的着色器阶段的输入。

在索引呈现的条带拓扑，如三角形条带，提供一种机制用于绘制与单个的多个带 * 绘制\*<em>（） 调用 (即，**剪切</em>* 剪切的命令条带）。

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置，并销毁 IA:

[**CalcPrivateElementLayoutSize**](https://msdn.microsoft.com/library/windows/hardware/ff538289)

[**CreateElementLayout**](https://msdn.microsoft.com/library/windows/hardware/ff540640)

[**DestroyElementLayout**](https://msdn.microsoft.com/library/windows/hardware/ff552771)

[**IaSetIndexBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff567387)

[**IaSetInputLayout**](https://msdn.microsoft.com/library/windows/hardware/ff567389)

[**IaSetTopology**](https://msdn.microsoft.com/library/windows/hardware/ff567390)

[**IaSetVertexBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff567392)

 

 





