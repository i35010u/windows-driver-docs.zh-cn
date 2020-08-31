---
title: 以追溯方式要求自由线程 CalcPrivate DDI
description: 以追溯方式要求自由线程 CalcPrivate DDI
ms.assetid: a25fbe8e-737a-4b47-8293-7cf13ebc8ac2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c586b18b0057f4a9b892318329432819dde049b6
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063482"
---
# <a name="retroactively-requiring-free-threaded-calcprivate-ddis"></a>以追溯方式要求自由线程 CalcPrivate DDI


Direct3D 版本11以追溯方式需要用户模式显示驱动程序函数，这些函数以 *pfnCalcPrivate* 的形式从具有自由线程的 Direct3D 版本 10 DDI 函数开始。 此追溯要求匹配 Direct3D 版本 11 DDI 的行为，该行为始终需要可自由线程的*pfnCalcPrivate \* *和[**pfnCalcDeferredContextHandleSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)函数，即使驱动程序指示它不支持 DDI 线程处理也是如此。 有关驱动程序如何指示线程支持的详细信息，请参阅 [支持线程处理、命令列表和三维管道](supporting-threading--command-lists--and-3-d-pipeline.md)。 此追溯要求的原因是，此类函数通常非常简单，因为它们返回的是大小的直接值。 更复杂的函数决定根据传递给函数的参数返回哪个即时值。 对于以 *pfnCalcPrivate* 开头的函数的要求，若要实际将任何数据写入堆栈以外的位置，则该函数不存在。 这些函数需要读取除参数以外的任何数据都是一个 rarity。 读取数据的任何要求都不会产生争用问题。 这一事实允许 Direct3D 版本 11 API 执行大量的优化，并防止每次创建 (执行开销高昂的同步，例如，任何调用来创建对象（如调用 [**CreateResource (D3D10) **](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource) 或 [**CreateGeometryShader**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshader)) ），而不是只使用一次。

此追溯自由线程需求的一个值得注意的例外是用于满足显示设备创建的 [**CalcPrivateDeviceSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize) 函数。 *CalcPrivateDeviceSize* 位于适配器函数表 ([**D3D10 \_ 2DDI \_ ADAPTERFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs) 或 [**D3D10DDI \_ ADAPTERFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_adapterfuncs)) 上。 *CalcPrivateDeviceSize* 不在遇到线程模型 relaxation 的函数组的下方。 无需对 *CalcPrivateDeviceSize* 函数进行自由线程。

 

