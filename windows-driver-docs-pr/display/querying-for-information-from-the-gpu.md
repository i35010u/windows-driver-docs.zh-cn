---
title: 从 GPU 查询信息
description: 从 GPU 查询信息
ms.assetid: 0d3942c2-3ae8-4eaa-9780-f146dd49699c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dc338e82077ca6ad066d13d93d88b9105cd379c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064640"
---
# <a name="querying-for-information-from-the-gpu"></a>从 GPU 查询信息


Direct3D 运行时可能需要图形处理单元中的信息 (GPU) ，而不是输出呈现目标或输出顶点缓冲区。 由于 GPU 与 CPU 并行执行，因此用户模式显示驱动程序应提供有效地向 GPU 提供异步通信的函数。

查询对象是运行时和驱动程序用于异步通知的资源。 若要创建查询对象，运行时首先调用驱动程序的 [**CalcPrivateQuerySize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatequerysize) 函数，以便驱动程序可以提供驱动程序所需的内存区域的大小。 然后，运行时调用驱动程序的 [**servicecontext.createquery (D3D10) **](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createquery) 函数来创建查询对象。 在*CalcPrivateQuerySize*和*servicecontext.createquery (D3D10) *调用中，运行时在*D3D10DDIARG 参数指向的* [**servicecontext.createquery \_ pCreateQuery**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createquery)结构的**查询**成员中[**提供查询类型 \_ **](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10ddi_query)值。

每个查询对象实例都存在于三种状态之一： *生成*、 *发出*和 *终止*。 运行时调用驱动程序的 [**QueryBegin**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querybegin) 函数，以将查询对象转换为生成状态。

**注意**   除 D3D10DDI *QueryBegin* \_ 查询 \_ 事件和 D3D10DDI \_ 查询 \_ 时间戳外，所有查询类型都支持 QueryBegin。 D3D10DDI \_ 查询 \_ 事件和 D3D10DDI \_ 查询 \_ 时间戳的构建概念不存在。

 

运行时调用驱动程序的 [**QueryEnd**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_queryend) 函数，以将查询对象转换为已发送状态。 转换到终止状态的时间晚于异步发生。 运行时调用驱动程序的 [**QueryGetData**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querygetdata) 函数来检测查询是否已转换为终止状态。 如果查询处于终止状态，则 *QueryGetData* 可以向后传递返回的数据，该数据适用于 *pData* 参数指向的内存区域中的查询。

同一类型的所有查询对象都是 FIFO (即先进先出) 。 例如，D3D10DDI query 事件类型的所有查询对象都按照 \_ \_ 其发出的顺序在 FIFO 顺序中完成。 但是，不同类型的查询对象可以完成或以重叠顺序表示。 例如，D3D10DDI 查询事件类型的查询 \_ \_ 可以在 D3D10DDI 查询封闭类型的查询之前完成 \_ \_ ，即使运行时在运行时发出了 \_ \_ D3D10DDI \_ query 封闭查询后发出了 D3D10DDI 查询事件查询 \_ 。

当运行时不再需要 query 对象时，运行时将释放以前为对象分配的内存区域，并调用驱动程序的 [**DestroyQuery (D3D10) **](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyquery) 函数，以通知驱动程序驱动程序不能再访问此内存区域。

 

