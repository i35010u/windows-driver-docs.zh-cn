---
title: 从 GPU 查询信息
description: 从 GPU 查询信息
ms.assetid: 0d3942c2-3ae8-4eaa-9780-f146dd49699c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 705262fcc7ddeda70ce8f9bb8df750d02ea6cc21
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826004"
---
# <a name="querying-for-information-from-the-gpu"></a>从 GPU 查询信息


Direct3D 运行时可能需要来自图形处理单元（GPU）而不是输出呈现器目标或输出顶点缓冲区的信息。 由于 GPU 与 CPU 并行执行，因此用户模式显示驱动程序应提供有效地向 GPU 提供异步通信的函数。

查询对象是运行时和驱动程序用于异步通知的资源。 若要创建查询对象，运行时首先调用驱动程序的[**CalcPrivateQuerySize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatequerysize)函数，以便驱动程序可以提供驱动程序所需的内存区域的大小。 然后，运行时调用驱动程序的[**servicecontext.createquery （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createquery)函数来创建查询对象。 在*CalcPrivateQuerySize*和*servicecontext.createquery （D3D10）* 调用中，运行时在[**D3D10DDIARG\_servicecontext.createquery**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createquery)的**query**成员中提供[**D3D10DDI\_查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10ddi_query)枚举的查询类型值。*pCreateQuery*参数指向的结构。

每个查询对象实例都存在于三种状态之一：*生成*、*发出*和*终止*。 运行时调用驱动程序的[**QueryBegin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querybegin)函数，以将查询对象转换为生成状态。

**请注意**   除了 D3D10DDI\_QUERY\_事件和 D3D10DDI\_查询\_时间戳外，所有查询类型都支持*QueryBegin* 。 D3D10DDI\_查询\_事件和 D3D10DDI\_查询\_时间戳的构建概念不存在。

 

运行时调用驱动程序的[**QueryEnd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_queryend)函数，以将查询对象转换为已发送状态。 转换到终止状态的时间晚于异步发生。 运行时调用驱动程序的[**QueryGetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querygetdata)函数来检测查询是否已转换为终止状态。 如果查询处于终止状态，则*QueryGetData*可以向后传递返回的数据，该数据适用于*pData*参数指向的内存区域中的查询。

同一类型的所有查询对象都是 FIFO （即先进先出）。 例如，D3D10DDI 类型的所有查询对象\_查询\_事件根据其发出的顺序在 FIFO 顺序中完成。 但是，不同类型的查询对象可以完成或以重叠顺序表示。 例如，类型为 D3D10DDI\_查询\_事件的查询可以在 D3D10DDI 类型\_查询\_封闭之前完成，即使运行时在运行时发出了 D3D10DDI\_查询\_事件查询D3D10DDI\_QUERY\_封闭查询。

当运行时不再需要 query 对象时，运行时将释放以前为对象分配的内存区域，并调用驱动程序的[**DestroyQuery （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyquery)函数以通知驱动程序驱动程序无法再访问此内存区域。

 

 





