---
title: 流输出阶段
description: 流输出阶段
ms.assetid: e3f4685f-a214-4934-a36f-92591ef99db8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5a38a254ed2cd613a84c62e5be78e80a96e321d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829435"
---
# <a name="stream-output-stage"></a>流输出阶段


流输出（因此）阶段可以在这些顶点到达光栅化人之前，将顶点流式传输到内存。 流输出的工作方式类似于管道中的点击操作。 即使数据继续向下传递到光栅器，也可以打开此点击。 通过流输出发送的数据会连接到缓冲区。 可以在后续传递中将这些缓冲区其中为管道输入。

一个有关流输出的约束是，将其绑定到几何图形着色器，因为它们必须一起创建（尽管可以是 "NULL"/"关闭"）。 不过，流式传输到的特定内存缓冲区不会绑定到特定的几何图形着色器和流输出对。 仅将对流输出的顶点数据的哪些部分的说明绑定到几何图形着色器。

流输出对于保存将重复使用的已排序管道数据可能很有用。 例如，一批顶点可以是 "skinned"，方法是将顶点传递到管道中，就像它们是独立点（只是一次访问所有这些顶点），对每个顶点应用 "皮" 操作，然后将结果流式传输到内存。 已保存的 "skinned" 顶点随后可用作输入。

由于通过流输出写入的输出量是动态的，因此需要一种新的绘图类型[**DrawAuto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_drawauto)，以允许流输出缓冲区与输入汇编程序一起重复使用，而无需 CPU 干预来确定数据量实际上已写入。 此外，查询还需要减少流输出溢出，并检索写入到流输出缓冲区的数据量（D3D10DDI\_查询\_STREAMOVERFLOWPREDICATE 和 D3D10DDI\_查询\_[**D3D10DDI\_查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10ddi_query)枚举）的 STREAMOUTPUTSTATS。

Direct3D 运行时调用以下驱动程序函数来创建和设置流输出：

[**CalcPrivateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivategeometryshaderwithstreamoutput)

[**CreateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshaderwithstreamoutput)

[**SoSetTargets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_so_settargets)

 

 





