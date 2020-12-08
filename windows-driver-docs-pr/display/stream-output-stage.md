---
title: 流输出阶段
description: 流输出阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a77e2d68c4a8568a0100e6070cd78a163c7f68c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831855"
---
# <a name="stream-output-stage"></a>流输出阶段


流输出 (因此) 阶段可以在这些顶点到达光栅人员之前将顶点流式传输到内存。 流输出的工作方式类似于管道中的点击操作。 即使数据继续向下传递到光栅器，也可以打开此点击。 通过流输出发送的数据会连接到缓冲区。 可以在后续传递中将这些缓冲区其中为管道输入。

一个有关流输出的约束是，将其绑定到几何图形着色器，因为它们必须一起创建 (但可以是 "NULL"/"off" ) 。 不过，流式传输到的特定内存缓冲区不会绑定到特定的几何图形着色器和流输出对。 仅将对流输出的顶点数据的哪些部分的说明绑定到几何图形着色器。

流输出对于保存将重复使用的已排序管道数据可能很有用。 例如，一批顶点可能是 "skinned"，因为顶点将顶点传递到管道中，就像它们是独立点 (只是一次访问所有它们) ，对每个顶点应用 "皮" 操作，然后将结果流式传输到内存。 已保存的 "skinned" 顶点随后可用作输入。

由于通过流输出写入的输出量是动态的，因此需要一种新的绘图类型 [**DrawAuto**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_drawauto)，以允许流输出缓冲区与输入汇编程序一起重复使用，而无需 CPU 干预来确定实际写入的数据量。 此外，还需要执行查询来减少流输出溢出，还需要检索将多少数据写入到流输出缓冲区 (D3D10DDI \_ query \_ STREAMOVERFLOWPREDICATE 和 D3D10DDI \_ Query \_ STREAMOUTPUTSTATS for [**D3D10DDI \_ query**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10ddi_query) 枚举) 。

Direct3D 运行时调用以下驱动程序函数来创建和设置流输出：

[**CalcPrivateGeometryShaderWithStreamOutput**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivategeometryshaderwithstreamoutput)

[**CreateGeometryShaderWithStreamOutput**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshaderwithstreamoutput)

[**SoSetTargets**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_so_settargets)

 

