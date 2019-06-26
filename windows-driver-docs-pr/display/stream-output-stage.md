---
title: 流输出阶段
description: 流输出阶段
ms.assetid: e3f4685f-a214-4934-a36f-92591ef99db8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68d6c9d68887d412a6c068c1471acaa84cf3648d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364361"
---
# <a name="stream-output-stage"></a>流输出阶段


输出 （因此） 之前这些顶点到达光栅器阶段可以流式传输出顶点到内存流。 流输出等 tap 管道中进行操作。 即使在数据会继续向下传递到光栅化程序，可开启此点击。 通过流输出发出的数据被连接到缓冲区。 这些缓冲区可以作为管道输入再循环在随后的遍历。

有关流的一个约束输出是与几何着色器，则必须在一起创建 (尽管可以是"NULL"/"关闭")。 尽管会传送给特定的内存缓冲区不被绑定到特定的几何着色器和流输出对。 仅说明的顶点数据输送到流的哪些部分输出绑定到几何着色器。

流输出可能适用于保存有序的管道会重复使用的数据。 例如，一批的顶点可能是"皮肤"通过将顶点传递到管道，就好像它们是独立的点 （只是为了一次访问所有这些操作）、 应用每个顶点上的"外观"操作和流式处理到内存的结果。 查看已保存的"控制外观"顶点会随后可供使用作为输入。

通过流输出写入的输出量是动态的因为新的绘图，类型[ **DrawAuto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_drawauto)，需要允许流输出缓冲区，而不重用与输入装配器若要确定实际写入的数据量的 CPU 参与。 此外，查询所需缓解流输出溢出，以及检索多少数据写入到流输出缓冲区 (D3D10DDI\_查询\_STREAMOVERFLOWPREDICATE 和 D3D10DDI\_查询\_STREAMOUTPUTSTATS [ **D3D10DDI\_查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3d10ddi_query)枚举)。

Direct3D 运行时调用以下的驱动程序函数，来创建和设置的流输出：

[**CalcPrivateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivategeometryshaderwithstreamoutput)

[**CreateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshaderwithstreamoutput)

[**SoSetTargets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_so_settargets)

 

 





